---
title: Utilisation de la publication sélective dans un média dynamique
description: Informations relatives à l’utilisation de la publication sélective dans les médias dynamiques.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
translation-type: tm+mt
source-git-commit: 4a144e53217c4353818d778415cc303b21412566
workflow-type: tm+mt
source-wordcount: '2934'
ht-degree: 6%

---


# Configuration de la publication sélective au niveau des dossiers dans Contenu multimédia dynamique {#selective-publish-configure-folder}

Vous pouvez choisir de publier ou d’annuler la publication de fichiers dans AEM ou dans Contenu multimédia dynamique au niveau du dossier, à l’aide de **[!UICONTROL Gérer la publication]** ou Publication **** rapide, plutôt que de vous reposer uniquement sur la configuration **[!UICONTROL du contenu multimédia]** dynamique dont les paramètres sont globaux pour tous les dossiers de votre instance Contenu multimédia dynamique.

Par exemple, avec la publication sélective, vous pouvez travailler sur des ressources pour des produits qui ne sont pas encore en ligne. Dans ce cas, une équipe marketing peut accéder à des images de recadrage intelligent et à des rendus dynamiques synchronisés dans Contenu multimédia dynamique afin de pouvoir créer du matériel promotionnel, sans avoir à publier ces ressources dans Contenu multimédia dynamique pour une diffusion globale.

>[!IMPORTANT]
>
>La fonction Publication sélective est disponible uniquement en mode Contenu multimédia dynamique - Scene7.

>[!NOTE]
>
>*La copie* de fichiers vers et depuis des dossiers efface l’état de publication de ces fichiers. Cependant, lorsque vous *déplacez* des fichiers vers et depuis des dossiers dont la propriété de dossier est définie sur Publication **** sélective, l’état de publication de ces fichiers est conservé.

Si vous décidez ultérieurement de modifier les paramètres de publication **** sélective dans un dossier, ces modifications n’affectent que les nouveaux fichiers que vous téléchargez vers ce dossier à partir de ce moment. L’état de publication des fichiers existants dans le dossier reste tel quel jusqu’à ce que vous les modifiiez manuellement à partir de la boîte de dialogue Publication **** rapide ou **[!UICONTROL Gérer la publication]** .

L’option Mode **[!UICONTROL de publication de médias]** dynamiques au niveau du dossier utilise toujours la valeur par défaut du paramètre **[!UICONTROL Publier les ressources]** de votre configuration de médias **[!UICONTROL dynamiques.]** Les étapes suivantes de cette rubrique vous montrent toutefois comment modifier manuellement cette valeur par défaut au niveau du dossier (comme décrit dans les étapes suivantes) pour remplacer la valeur Configuration **[!UICONTROL de média]** dynamique.

Que vous utilisiez la valeur **[!UICONTROL Publier les ressources]** définie dans Configuration **** dynamique des médias ou la valeur du mode **[!UICONTROL Publication de médias]** dynamique définie dans les propriétés au niveau du dossier, vous pouvez toujours choisir l’option **[!UICONTROL Immédiatement, A l’Activation ou Publier de manière sélective.]********** Par exemple, vous pouvez définir la valeur **[!UICONTROL Publier les ressources]** dans votre configuration **[!UICONTROL de médias]** dynamiques sur **[!UICONTROL À l’Activation]**, mais définissez la valeur du mode Publication de médias **[!UICONTROL dynamiques au niveau du dossier sur Publication sélective, inversement, etc.]******

Après avoir configuré la publication sélective dans un dossier, vous pouvez effectuer l’une des opérations suivantes :

* [Publiez sélectivement des fichiers dans Contenu multimédia dynamique ou AEM à l’aide de la fonction Gérer la publication.](#selective-publish-manage-publication)
* [Annulation sélective de la publication de fichiers issus de Contenu multimédia dynamique ou d’AEM à l’aide de la fonction Gérer la publication.](#selective-unpublish-manage-publication)
* [Publication de fichiers dans Contenu multimédia dynamique ou AEM à l’aide de la publication rapide.](#quick-publish-aem-dm)
* [Publiez ou annulez sélectivement des fichiers au moyen des résultats de la recherche.](#selective-publish-unpublish-search-results)

**Pour configurer la publication sélective au niveau des dossiers dans Contenu multimédia dynamique**

1. Dans AEM, appuyez sur le logo AEM pour accéder à la console de navigation globale. Sur le côté gauche, appuyez sur l’icône Navigation (juste au-dessus de l’icône Outils), puis appuyez sur **[!UICONTROL Ressources > Fichiers.]**
1. Utilisez l’une des méthodes suivantes :
   * Modifiez les propriétés d&#39;un dossier existant. Dans la Vue **[!UICONTROL de]** carte, la Vue **[!UICONTROL de]** colonne ou la Vue **[!UICONTROL de]** Liste, accédez à un dossier dont vous souhaitez modifier les propriétés. Sélectionnez le dossier, puis sur la barre d’outils, appuyez sur **[!UICONTROL Propriétés.]**
   * Modifiez les propriétés d’un nouveau dossier - Dans la Vue **[!UICONTROL de]** carte, la Vue **[!UICONTROL de]** colonne ou la Vue **[!UICONTROL de]** Liste, près du coin supérieur droit de la page, appuyez sur **[!UICONTROL Créer > Dossier.]** Dans la boîte de dialogue **[!UICONTROL Créer un dossier]** , saisissez un titre (obligatoire) pour le dossier, puis appuyez sur **[!UICONTROL Créer.]** Sélectionnez le dossier, puis sur la barre d’outils, appuyez sur **[!UICONTROL Propriétés.]**

1. Dans la liste déroulante Mode **[!UICONTROL de]** synchronisation, sélectionnez l’une des options suivantes :

   | Mode de synchronisation | Description |
   | --- | --- |
   | **[!UICONTROL Hérité]** | No explicit sync value on the folder; instead, the folder inherits the sync value from one of its ancestor folders or the default mode set in your **[!UICONTROL Dynamic Media Configuration.]** L’état détaillé de l’état **[!UICONTROL hérité]** s’affiche au moyen d’une info-bulle. |
   | **[!UICONTROL Synchroniser avec Dynamic Media tout le contenu de cette sous-arborescence de dossiers]** | Pour que la publication sur Contenu multimédia dynamique réussisse, les ressources doivent être synchronisées sur Contenu multimédia dynamique. La sélection de cette option inclura tous les actifs de cette sous-arborescence pour la synchronisation avec Contenu multimédia dynamique. Les paramètres propres au dossier remplacent le paramètre par défaut dans la configuration **[!UICONTROL dynamique des médias.]** |
   | **[!UICONTROL Exclure tout ce qui se trouve dans cette sous-arborescence de dossiers de la synchronisation dynamique des médias]** | Exclure la synchronisation de tous les fichiers de cette sous-arborescence vers Contenu multimédia dynamique. |

   ![Publication sélective au niveau du dossier](/help/assets/assets-dm/createfolder-properties-selectivepublish.png)

1. Dans la liste déroulante Mode **[!UICONTROL de publication de médias]** dynamiques, sélectionnez une option. Gardez à l’esprit que l’option Mode **[!UICONTROL de publication de médias]** dynamiques utilise toujours par défaut la valeur définie dans la configuration de médias **[!UICONTROL dynamiques.]** Vous pouvez toutefois remplacer manuellement cette valeur de configuration **[!UICONTROL de média]** dynamique par défaut à l’aide de l’une des options suivantes.

   >[!IMPORTANT]
   >
   >Gardez à l’esprit que, quelle que soit l’option de mode de publication de contenu multimédia dynamique sélectionnée, les mises à jour apportées ultérieurement à un fichier *déjà* publié sont immédiatement publiées sans autre action de l’utilisateur.

   | Mode de publication de médias dynamiques, option | Description |
   | --- | --- |
   | **[!UICONTROL Immédiatement]** | Lorsque des fichiers sont téléchargés dans ce dossier, le système les ingère dans AEM et fournit instantanément l’URL/l’incorporation. Cette option est liée à AEM publication uniquement et aucune intervention de l’utilisateur n’est nécessaire pour publier des fichiers.<br>Cette option *n’est pas* disponible si vous avez sélectionné **[!UICONTROL Exclure tout ce qui se trouve dans cette sous-arborescence de dossiers de la synchronisation]** dynamique des médias en mode **** Sync à l’étape précédente. |
   | **[!UICONTROL Lors de l’activation]** | Lorsque des fichiers sont téléchargés dans ce dossier, vous devez d’abord publier explicitement le fichier avant de fournir un lien URL/incorporé. Cette option est liée à AEM publication uniquement.<br>Cette option *n’est pas* disponible si vous avez sélectionné **[!UICONTROL Exclure tout ce qui se trouve dans cette sous-arborescence de dossiers de la synchronisation]** dynamique des médias en mode **** Sync à l’étape précédente. |
   | **[!UICONTROL Publication sélective]** | Les fichiers sont publiés à votre choix, AEM ou Contenu multimédia dynamique, pour diffusion dans le domaine public. Les deux méthodes de publication s’excluent mutuellement.  En d’autres termes, vous pouvez publier des fichiers dans DMS7 afin d’utiliser des fonctionnalités telles que Recadrage dynamique ou Rendus dynamiques. Or, you can publish assets exclusively to AEM for secure previewing; those same assets are *not* published to DMS7 for delivery in the public domain. Cette option n’est pas disponible si vous avez sélectionné **[!UICONTROL Exclure tout ce qui se trouve dans cette sous-arborescence de dossiers de la synchronisation]** dynamique des médias en mode **** synchronisation à l’étape précédente. |

1. Dans le coin supérieur droit de la page, appuyez sur **[!UICONTROL Enregistrer et fermer]**, puis sur **[!UICONTROL OK]** pour revenir à AEM Assets.

## Publication sélective de fichiers dans un média dynamique ou AEM à l’aide de la fonction Gérer la publication{#selective-publish-manage-publication}

Avant de pouvoir utiliser **[!UICONTROL Gérer la publication]** pour publier des fichiers de manière sélective dans Contenu multimédia dynamique ou AEM, assurez-vous d’avoir défini l’option **[!UICONTROL Publier les ressources]** dans Configuration **[!UICONTROL de Contenu multimédia]** **[!UICONTROL dynamique sur Publication sélective ou configuré la publication sélective au niveau du dossier.]**

Voir [Création d’une configuration](#configuring-dynamic-media-cloud-services) de contenu multimédia dynamique ou [Configuration d’une publication sélective au niveau des dossiers dans Contenu multimédia dynamique.](#selective-publish-configure-folder)

>[!IMPORTANT]
>
>La fonction Publication sélective est disponible uniquement en mode Contenu multimédia dynamique - Scene7.

>[!NOTE]
>
>*La copie* de fichiers vers et depuis des dossiers efface l’état de publication de ces fichiers. Cependant, lorsque vous *déplacez* des fichiers vers et depuis des dossiers dont la propriété de dossier est définie sur Publication **** sélective, l’état de publication de ces fichiers est conservé.

**Pour publier de manière sélective des fichiers dans un média dynamique ou AEM à l’aide de la commande Gérer la publication**

1. Dans AEM, appuyez sur le logo AEM pour accéder à la console de navigation globale. Sur le côté gauche, appuyez sur l’icône Navigation (juste au-dessus de l’icône Outils), puis appuyez sur **[!UICONTROL Ressources > Fichiers.]**
1. Dans la Vue **[!UICONTROL de]** carte, la Vue **[!UICONTROL de]** colonnes ou la Vue **[!UICONTROL de]** Liste, effectuez l’une des opérations suivantes :
   * Accédez à un dossier dont vous souhaitez publier les fichiers. Sélectionnez le dossier, puis sur la barre d’outils, appuyez sur **[!UICONTROL Gérer la publication.]**  Il peut s’avérer utile d’utiliser la Vue **[!UICONTROL de]** Liste pour vérifier plus facilement l’état de publication d’un dossier particulier.
   * Accédez à un dossier dont vous souhaitez publier les fichiers. Ouvrez le dossier, puis sélectionnez un ou plusieurs fichiers. On the toolbar, tap **[!UICONTROL Manage Publication.]** Il peut s’avérer utile d’utiliser la Vue **[!UICONTROL de]** Liste afin de vérifier plus facilement l’état de publication d’un fichier particulier.

      >[!NOTE]
      >
      >Si **[!UICONTROL Gérer la publication]** n’est pas visible dans la barre d’outils, appuyez sur le bouton d’ellipse à la place, puis sélectionnez **[!UICONTROL Gérer la publication]** dans le menu liste.

1. Dans la page **[!UICONTROL Gérer la publication - Options]** , sous **[!UICONTROL Action]**, sélectionnez le type d’activation souhaité.

   | Action | Description |
   | --- | --- |
   | **[!UICONTROL Publier]** (vers AEM) | Sélectionnez cette option pour publier des fichiers sur AEM pour une prévisualisation sécurisée. |
   | **[!UICONTROL Publier vers Dynamic Media]** | Sélectionnez cette option pour publier des fichiers dans Contenu multimédia dynamique pour diffusion dans le domaine public ou pour utiliser des fonctionnalités telles que Recadrage dynamique ou Rendus dynamiques.<br>Cette option est disponible uniquement si le mode **[!UICONTROL Publication de médias]** dynamiques est défini sur Publication **** sélective dans les propriétés du dossier. |

1. Sous **[!UICONTROL Planification]**, définissez le calendrier de publication.

   | Planification | Description |
   | --- | --- |
   | **[!UICONTROL Maintenant]** | Sélectionnez cette option pour publier immédiatement les fichiers. |
   | **[!UICONTROL Plus tard]** | Sélectionnez cette option pour publier les fichiers à une date et une heure données. |

1. In the upper-right corner of the **[!UICONTROL Manage Publication]** page, tap **[!UICONTROL Next.]**
1. Dans la page **[!UICONTROL Gérer la publication - Portée]** , effectuez l’une des opérations suivantes :
   * Si nécessaire, sélectionnez un ou plusieurs fichiers à supprimer de la publication.
   * Dans le coin supérieur droit de la page **[!UICONTROL Gérer la publication - Portée]** , appuyez sur **[!UICONTROL Publier]** ou **[!UICONTROL Publier dans le contenu multimédia dynamique.]**
1. Appuyez sur **[!UICONTROL OK.]**

### Annulation sélective de la publication de fichiers issus de Contenu multimédia dynamique ou d’AEM à l’aide de la fonction Gérer la publication {#selective-unpublish-manage-publication}

1. Dans AEM, appuyez sur le logo AEM pour accéder à la console de navigation globale. Sur le côté gauche, appuyez sur l’icône Navigation (juste au-dessus de l’icône Outils), puis appuyez sur **[!UICONTROL Ressources > Fichiers.]**
1. Dans la Vue **[!UICONTROL de]** carte, la Vue **[!UICONTROL de]** colonnes ou la Vue **[!UICONTROL de]** Liste, effectuez l’une des opérations suivantes :
   * Accédez au dossier dont vous souhaitez annuler la publication. Sélectionnez le dossier, puis sur la barre d’outils, appuyez sur **[!UICONTROL Gérer la publication.]**  Il peut s’avérer utile d’utiliser la Vue **[!UICONTROL de]** Liste pour vérifier plus facilement l’état de publication d’un dossier particulier.
   * Accédez au dossier dont vous souhaitez annuler la publication. Ouvrez le dossier, puis sélectionnez un ou plusieurs fichiers. On the toolbar, tap **[!UICONTROL Manage Publication.]** Il peut s’avérer utile d’utiliser la Vue **[!UICONTROL de]** Liste afin de vérifier plus facilement l’état de publication d’un fichier particulier.

      >[!NOTE]
      >
      >Si **[!UICONTROL Gérer la publication]** n’est pas visible dans la barre d’outils, appuyez sur le bouton d’ellipse à la place, puis sélectionnez **[!UICONTROL Gérer la publication]** dans le menu liste.

1. Dans la page **[!UICONTROL Gérer la publication - Options]** , sous **[!UICONTROL Action]**, sélectionnez le type de désactivation souhaité.

   | Action | Description |
   | --- | --- |
   | **[!UICONTROL Annuler la publication]** (à partir de AEM) | Sélectionnez cette option pour annuler la publication des fichiers AEM. |
   | **[!UICONTROL Annuler la publication à partir de Dynamic Media]** | Sélectionnez cette option pour annuler la publication de fichiers dans Contenu multimédia dynamique.<br>Cette option est disponible uniquement si le mode **[!UICONTROL Publication de médias]** dynamiques est défini sur Publication **** sélective dans les propriétés du dossier. |

1. Sous **[!UICONTROL Planification]**, définissez le moment de la désactivation.

   | Planification | Description |
   | --- | --- |
   | **[!UICONTROL Maintenant]** | Sélectionnez cette option pour annuler immédiatement la publication des fichiers. |
   | **[!UICONTROL Plus tard]** | Sélectionnez cette option pour annuler la publication des fichiers à une date et une heure données. |

1. In the upper-right corner of the **[!UICONTROL Manage Publication]** page, tap **[!UICONTROL Next.]**
1. Dans la page **[!UICONTROL Gérer la publication - Portée]** , effectuez l’une des opérations suivantes :
   * Sélectionnez un ou plusieurs fichiers à supprimer de l’annulation de publication.
   * Dans le coin supérieur droit de la page **[!UICONTROL Gérer la publication - Portée]** , appuyez sur **[!UICONTROL Annuler la publication]** ou **[!UICONTROL Annuler la publication dans Contenu multimédia dynamique.]**
1. Appuyez sur **[!UICONTROL OK.]**

## Publication de fichiers dans Contenu multimédia dynamique ou AEM à l’aide de la publication rapide {#quick-publish-aem-dm}

Vous pouvez utiliser la fonction Publication **** rapide pour des cas d’activation de ressources simples. **[!UICONTROL Quick Publish]** publie immédiatement les ressources sélectionnées sans autre interaction de l’utilisateur. Par conséquent, toutes les références non publiées sont également publiées automatiquement.

>[!NOTE]
>
>Pour utiliser la publication **** rapide pour publier des fichiers dans Contenu multimédia dynamique ou AEM, veillez à ce que la publication **** sélective soit activée dans votre configuration **[!UICONTROL de Contenu multimédia]** dynamique ou dans les propriétés de dossier du dossier sélectionné.

**Pour publier des fichiers dans Contenu multimédia dynamique ou AEM à l’aide de la fonction Publication rapide**

1. Dans AEM, appuyez sur le logo AEM pour accéder à la console de navigation globale. Sur le côté gauche de la page, appuyez sur l’icône Navigation (juste au-dessus de l’icône Outils), puis sur le côté droit de la page, appuyez sur **[!UICONTROL Ressources > Fichiers.]**
1. Dans la Vue **[!UICONTROL de]** carte, la Vue **[!UICONTROL de]** colonnes ou la Vue **[!UICONTROL de]** Liste, effectuez l’une des opérations suivantes :
   * Accédez à un dossier dont vous souhaitez publier les fichiers. Sélectionnez le dossier, puis sur la barre d’outils, appuyez sur Publication **[!UICONTROL rapide.]**  Il peut s’avérer utile d’utiliser la Vue **[!UICONTROL de]** Liste pour vérifier plus facilement l’état de publication d’un dossier particulier.
   * Accédez à un dossier dont vous souhaitez publier les fichiers. Ouvrez le dossier, puis sélectionnez un ou plusieurs fichiers. Dans la barre d’outils, appuyez sur **[!UICONTROL Publication rapide.]** Il peut s’avérer utile d’utiliser la Vue **[!UICONTROL de]** Liste afin de vérifier plus facilement l’état de publication d’un fichier particulier.

      >[!NOTE]
      >
      >Si Publication **** rapide n’est pas visible dans la barre d’outils, appuyez sur le bouton d’ellipse à la place, puis sélectionnez Publication **** rapide dans le menu liste.

      ![Publication rapide au niveau du dossier dans un média dynamique](/help/assets/assets-dm/selective-publish-folder-quick-publish-to-dm.png)

1. Sélectionnez l’une des options suivantes dans la liste de menu Publication **** rapide.

   | Publication rapide, option | Effets |
   | --- | --- | 
   | Publier sur AEM | Publie immédiatement les fichiers sélectionnés sur AEM. |
   | Publier sur Brand Portal | Publie immédiatement les fichiers sélectionnés sur le portail **[!UICONTROL de marques.]**<br>Cette option n’est disponible que si votre instance AEM Assets dispose déjà de**[!UICONTROL  Brand Portal ]**configuré. |
   | Publier vers Dynamic Media | Publie immédiatement les fichiers sélectionnés dans Contenu multimédia dynamique.<br>Un fichier doit déjà être synchronisé dans Contenu multimédia dynamique. Si nécessaire, assurez-vous que le mode **** Sync des propriétés d’un dossier est déjà défini pour **[!UICONTROL synchroniser tout ce qui se trouve dans cette sous-arborescence de dossiers sur dynamicmedia.]** |

1. Appuyez sur **[!UICONTROL OK]**, puis sur **[!UICONTROL Fermer.]**

## Publier ou annuler la publication sélective des fichiers au moyen des résultats de la recherche {#selective-publish-unpublish-search-results}

Les résultats de la recherche peuvent afficher des fichiers provenant de différents dossiers de fichiers dont les paramètres de publication dans Contenu multimédia dynamique sont différents. Lorsque vous avez sélectionné un ou plusieurs fichiers à partir des résultats de la recherche et que les fichiers ont des paramètres de mode de publication de Contenu multimédia dynamique différents, vous pouvez déclencher la publication **** Gérer la publication à partir de la barre d’outils, afin de publier ou d’annuler la publication.

Voir aussi [Rechercher des ressources dans AEM.](/help/assets/search-assets.md)

**Pour publier ou annuler la publication sélective de fichiers au moyen des résultats de la recherche**

1. En AEM, dans le coin supérieur gauche de la page, appuyez sur le logo AEM pour accéder à la console de navigation globale. Sur le côté gauche de la page, appuyez sur l’icône Navigation (juste au-dessus de l’icône Outils), puis appuyez sur **[!UICONTROL Ressources > Fichiers.]**
1. Dans la barre d’outils, près du coin supérieur droit de la page, appuyez sur l’icône Rechercher (loupe).
1. Dans le champ **[!UICONTROL Type à rechercher]** , entrez un mot-clé, puis appuyez sur **[!UICONTROL Entrée.]**
1. Près du coin supérieur droit de la page, appuyez sur l’icône de Vue **[!UICONTROL de]** Liste.
1. Near the upper-left corner of the page, tap the **[!UICONTROL Filters]** icon.

   ![Vue de liste et Filtres dans les résultats de la recherche](/help/assets/assets-dm/select-publish-search-result.png)

1. Dans le panneau de gauche, développez **[!UICONTROL Etat]**, puis développez le prédicat de recherche **[!UICONTROL Contenu multimédia]** dynamique.
1. Utilisez les cases à cocher **[!UICONTROL Publié]** et **[!UICONTROL Non publié]** pour affiner davantage les résultats de recherche en fonction de l’état publié des ressources Contenu multimédia dynamique.
Vous pouvez éventuellement utiliser ces cases à cocher conjointement avec le prédicat de recherche **[!UICONTROL Publier]** pour affiner les résultats de recherche des ressources AEM **[!UICONTROL publiées]** et **[!UICONTROL non publiées]** .
1. Utilisez l’une des méthodes suivantes :
   * Sélectionnez un ou plusieurs fichiers que vous souhaitez publier ou annuler la publication.
   * Près du coin supérieur droit de la page Résultats **[!UICONTROL de la]** recherche, appuyez sur **[!UICONTROL Sélectionner tout.]**
1. On the toolbar, tap **[!UICONTROL Manage Publication.]** Vous devrez peut-être appuyer sur l’icône représentant des points de suspension dans la barre d’outils pour afficher **[!UICONTROL Gérer la publication.]**
1. Sur la page **[!UICONTROL Gérer la publication - Options]** , sélectionnez l’action de votre choix.

   | Action sélectionnée | Paramètre Publier les ressources dans la configuration de Contenu multimédia dynamique | Les ressources sont |
   | --- | --- | --- |
   | Publication  | Immédiatement ou A l&#39;Activation | Publié sur AEM et Contenu multimédia dynamique. |
   | Publication  | Publication sélective | Publié sur AEM uniquement. |
   | Annuler la publication | Immédiatement ou A l&#39;Activation | Non publié à partir d’AEM et de Contenu multimédia dynamique. |
   | Annuler la publication | Publication sélective | Non publié à partir d&#39;AEM uniquement. |
   | Publier vers Dynamic Media | Immédiatement ou A l&#39;Activation | Non publié sur AEM, Contenu multimédia dynamique ou les deux. |
   | Publier vers Dynamic Media | Publication sélective | Publié dans Contenu multimédia dynamique uniquement. |
   | Annuler la publication à partir de Dynamic Media | Immédiatement ou A l&#39;Activation | Non annulé de la publication à partir d’AEM, de Contenu multimédia dynamique ou des deux. |
   | Annuler la publication à partir de Dynamic Media | Publication sélective | Annulation de la publication à partir de Contenu multimédia dynamique uniquement. |

1. Sous **[!UICONTROL Planification]**, définissez le moment de la désactivation.

   | Calendrier sélectionné | Ce qui se produit |
   | --- | --- |
   | Maintenant | L’action sélectionnée est exécutée immédiatement. |
   | Plus tard | L&#39;action sélectionnée est exécutée à la date et à l&#39;heure particulières sélectionnées. |

1. Dans le coin supérieur droit de la page **[!UICONTROL Gérer la publication - Options]** , appuyez sur **[!UICONTROL Suivant.]**
1. (Facultatif) Dans la page **[!UICONTROL Gérer la publication - Portée]** , passez en revue la colonne **[!UICONTROL Publier la Cible]** du tableau pour les ressources sélectionnées.

   | Paramètre Publier les ressources dans la configuration de Contenu multimédia dynamique | Action sélectionnée | Cible de publication |
   | --- | --- | --- |
   | Immédiatement ou <br>à l&#39;Activation | Publication  | aem et contenu multimédia dynamique |
   | Immédiatement ou <br>à l&#39;Activation | Publier vers Dynamic Media | Aucune |
   | Publication sélective | Publication  | AEM |
   | Publication sélective | Publier vers Dynamic Media | Dynamic Media |
   | Immédiatement ou <br>à l&#39;Activation | Annuler la publication | aem et contenu multimédia dynamique |
   | Immédiatement ou <br>à l&#39;Activation | Annuler la publication à partir de Dynamic Media | Aucune |
   | Publication sélective | Annuler la publication | AEM |
   | Publication sélective | Annuler la publication à partir de Dynamic Media | Dynamic Media |

1. Dans la page **[!UICONTROL Gérer la publication - Portée]** , effectuez l’une des opérations suivantes :
   * Sélectionnez un ou plusieurs fichiers à supprimer de la publication ou de l’annulation de publication.
   * Dans le coin supérieur droit de la page **[!UICONTROL Gérer la publication - Portée]** , appuyez sur **[!UICONTROL Publier]** ou **[!UICONTROL Annuler la publication]** pour lancer l’action.
1. Appuyez sur **[!UICONTROL OK.]**

## Vérification de l’état de publication d’un fichier {#check-publish-status-of-asset}

Vous pouvez utiliser le **[!UICONTROL journal]** avec la vue **[!UICONTROL de]** carte, la Vue **[!UICONTROL de]** colonne ou la Vue de **[!UICONTROL Liste dans AEM pour vérifier rapidement l’état de publication d’un fichier.]**

**Pour vérifier l’état de publication d’un fichier**

1. En AEM, dans le coin supérieur gauche de la page, appuyez sur le logo AEM pour accéder à la console de navigation globale. Sur le côté gauche de la page, appuyez sur l’icône Navigation (juste au-dessus de l’icône Outils), puis appuyez sur **[!UICONTROL Ressources > Fichiers.]**
1. Dans la Vue **[!UICONTROL de]** carte, la Vue **[!UICONTROL de]** colonnes ou la Vue **[!UICONTROL de]** Liste (capture d’écran ci-dessous montre la Vue de **[!UICONTROL Liste), ouvrez un dossier contenant les fichiers que vous avez publiés ou non publiés.]**
1. Sélectionnez un fichier pour qu’il s’affiche avec une coche. Voir la capture d’écran ci-dessous, par exemple.
1. Near the upper-left corner of the page, from the drop-down menu, select **[!UICONTROL Timeline.]** La région **[!UICONTROL Etat]** du panneau de gauche affiche l’état de publication de la ressource sélectionnée.
Lorsque vous utilisez la Vue **[!UICONTROL de]** Liste, une colonne supplémentaire pour l’état de publication **[!UICONTROL Contenu multimédia]** dynamique s’affiche.
   * Un dossier configuré pour la synchronisation avec Contenu multimédia dynamique affiche la colonne Contenu multimédia **** dynamique par défaut.
   * Un dossier *non* configuré pour la synchronisation avec Contenu multimédia dynamique n’affiche pas la colonne Contenu multimédia dynamique.
      ![Vue de liste et chronologie](/help/assets/assets-dm/selective-publish-status-timeline.png)

## Dépannage de la publication sélective {#selective-publish-troubleshoot}

Une ressource qui n’est pas synchronisée avec Contenu multimédia dynamique mais dont l’action de publication Contenu multimédia dynamique est déclenchée déclenche le message d’erreur et la solution suivante :

![Erreur de publication sélective](/help/assets/assets-dm/selective-publish-error.png)

