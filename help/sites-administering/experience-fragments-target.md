---
title: Exportation de fragments d’expérience vers Adobe Target
seo-title: Exporting Experience Fragments to Adobe Target
description: Exportation de fragments d’expérience vers Adobe Target
seo-description: Exporting Experience Fragments to Adobe Target
uuid: 2df0faab-5d5e-4fc1-93b3-28b7e6f3c306
contentOwner: carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: d4152b4d-531b-4b62-8807-a5bc5afe94c6
docset: aem65
exl-id: f2921349-de8f-4bc1-afa2-aeace99cfc5c
source-git-commit: a33d46bcfcf901fb774b742c0fc972265401a56e
workflow-type: tm+mt
source-wordcount: '1223'
ht-degree: 46%

---

# Exportation de fragments d’expérience vers Adobe Target{#exporting-experience-fragments-to-adobe-target}

>[!CAUTION]
>
>Certaines fonctionnalités de cette page nécessitent l’application d’AEM 6.5.3.0 (ou version ultérieure).
>
>6.5.3.0 :
>
>* **Domaines Externalizer** peut maintenant être sélectionné.
   >  **Remarque :** Les domaines de l’externaliseur ne sont pertinents que pour le contenu du fragment d’expérience envoyé à Target, et non pour les métadonnées telles que Afficher le contenu de l’offre.
>
>6.5.2.0:
>
>* Les fragments d’expérience peuvent être exportés vers :
   >
   >   * l’espace de travail par défaut.
   >   * un espace de travail nommé, spécifié dans la configuration cloud.
   >   * **Remarque :** L’exportation vers des espaces de travail spécifiques nécessite Adobe Target Premium.
>
>* AEM doit être [intégré à Adobe Target à l’aide d’Adobe I/O](/help/sites-administering/integration-target-ims-adobe-io.md).
>
>AEM 6.5.0.0 et 6.5.1.0 :
>
>* Les fragments d’expérience AEM sont exportés dans l’espace de travail par défaut d’Adobe Target.
>* AEM doit être intégré à Adobe Target conformément aux instructions de la section [Intégration à Adobe Target](/help/sites-administering/target.md).


Vous pouvez exporter [Fragments d’expérience](/help/sites-authoring/experience-fragments.md), créé dans Adobe Experience Manager (AEM), dans Adobe Target (Target). Ceux-ci peuvent ensuite être utilisés comme offres dans les activités Target, pour tester et personnaliser les expériences en fonction des besoins.

Il existe trois options de format pour exporter un fragment d’expérience vers Adobe Target :

* HTML (par défaut) : Prise en charge de la diffusion de contenu web et hybride
* JSON : Prise en charge de la diffusion de contenu sans interface
* HTML et JSON

Les fragments d’expérience AEM peuvent être exportés vers l’espace de travail par défaut dans Adobe Target ou vers des espaces de travail définis par l’utilisateur pour Adobe Target. Cela se fait par Adobe I/O, pour lequel AEM doit être [intégré à Adobe Target à l’aide d’Adobe I/O](/help/sites-administering/integration-target-ims-adobe-io.md).

>[!NOTE]
>
>Les espaces de travail Adobe Target n’existent pas dans Adobe Target lui-même. Ils sont définis et gérés dans Adobe IMS (système Identity Management), puis sélectionnés pour une utilisation dans toutes les solutions à l’aide des intégrations Adobe I/O.

>[!NOTE]
>
>Les espaces de travail Adobe Target peuvent être utilisés pour permettre aux membres d’une organisation (groupe) de créer et de gérer des offres et des activités pour cette organisation uniquement ; sans donner accès à d’autres utilisateurs. Par exemple, les organisations spécifiques à un pays dans une préoccupation mondiale.

>[!NOTE]
>
>Pour plus d’informations, voir aussi :
>
>* [Développement d’Adobe Target](https://www.adobe.io/apis/experiencecloud/target.html)
>* [Composants principaux - Fragments d’expérience](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/experience-fragment.html)
>


## Prérequis {#prerequisites}

>[!CAUTION]
>
>Certaines fonctionnalités de cette page nécessitent l’application d’AEM 6.5.3.0.

Plusieurs actions sont requises :

1. Vous devez [intégrer des AEM à Adobe Target à l’aide d’Adobe I/O](/help/sites-administering/integration-target-ims-adobe-io.md).
2. Les fragments d’expérience sont exportés à partir de l’instance d’auteur AEM. Vous devez donc [Configuration de l’externaliseur de liens d’AEM](/help/sites-administering/target-requirements.md#configuring-the-aem-link-externalizer) sur l’instance d’auteur pour vous assurer que toutes les références contenues dans le fragment d’expérience sont externalisées pour la diffusion web.

   >[!NOTE]
   >
   >Pour la réécriture de liens, non couverte par le format par défaut, il existe un [fournisseur de réécriture de liens des fragments d’expérience](/help/sites-developing/experience-fragments.md#the-experience-fragment-link-rewriter-provider-html). Cela vous permet de développer des règles personnalisées pour votre instance.

## Ajout de la configuration du cloud {#add-the-cloud-configuration}

Avant d’exporter un fragment, vous devez ajouter la **configuration cloud** pour **Adobe Target** au fragment ou au dossier. Vous pouvez ainsi :

* spécifier la ou les options de format à utiliser pour l&#39;export ;
* sélectionner un espace de travail Target comme destination
* sélectionner un domaine externaliseur pour réécrire des références dans le fragment d’expérience (facultatif) ;

Vous pouvez sélectionner les options obligatoires dans les **propriétés de page** du dossier ou du fragment concerné. La spécification sera héritée, le cas échéant.

1. Accédez à la console **Fragments d’expérience**.

1. Ouvrez les **propriétés de page** pour le dossier ou le fragment approprié.

   >[!NOTE]
   >
   >Lorsque vous ajoutez la configuration cloud au dossier parent du fragment d’expérience, celle-ci est héritée par tous les enfants.
   >
   >
   >Lorsque vous ajoutez la configuration cloud directement au fragment d’expérience, la configuration est héritée par toutes les variations.

1. Sélectionnez l’onglet **Services cloud**.

1. Sous **Configuration du Cloud Service**, sélectionnez **Adobe Target** dans la liste déroulante.

   >[!NOTE]
   >
   >Le format JSON d’une offre de fragment d’expérience peut être personnalisé. Pour ce faire, définissez un composant de fragment d’expérience client, puis annotez comment exporter ses propriétés dans le modèle Sling du composant.
   >
   >Voir le composant principal :
   >
   >[Composants principaux - Fragments d’expérience](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/experience-fragment.html)

   Sous **Adobe Target** select :

   * la configuration appropriée ;
   * l’option de format requise
   * un espace de travail Adobe Target
   * si nécessaire : domaine de l’externaliseur

   >[!CAUTION]
   >
   >Le domaine de l’externaliseur est facultatif.
   >
   > Un externaliseur d’AEM est configuré lorsque vous souhaitez que le contenu exporté pointe vers un *publier* domaine. Pour plus d’informations, voir [Configuration de l’externaliseur de liens d’AEM](/help/sites-administering/target-requirements.md#configuring-the-aem-link-externalizer).
   >
   > Notez également que les domaines Externalizer ne sont pertinents que pour le contenu du fragment d’expérience envoyé à Target, et non pour les métadonnées telles que Afficher le contenu de l’offre.

   Par exemple, pour un dossier :

   ![Dossier - Cloud Services](assets/xf-target-integration-01.png "Dossier - Cloud Services")

1. **Enregistrez et fermez**.

## Exportation d’un fragment d’expérience vers Adobe Target {#exporting-an-experience-fragment-to-adobe-target}

>[!CAUTION]
>
>Pour les contenus multimédias, comme les images, une seule référence est exportée vers Target. La ressource elle-même reste stockée dans AEM Assets et elle est diffusée depuis l’instance de publication AEM.
>
>Le fragment d’expérience, ainsi que l’ensemble des ressources connexes, doivent être publiés avant l’exportation vers Target.

Pour exporter un fragment d’expérience d’AEM vers Target (une fois la configuration cloud spécifiée) :

1. Accédez à la console Fragment d’expérience.
1. Sélectionnez le fragment d’expérience que vous souhaitez exporter vers Target.

   >[!NOTE]
   >
   >Il doit s’agir d’une variation web de fragment d’expérience.

1. Appuyez/cliquez sur **Exporter vers Adobe Target**.

   >[!NOTE]
   >
   >Si le fragment d’expérience a déjà été exporté, sélectionnez **Mettre à jour dans Adobe Target**.

1. Appuyez/cliquez sur **Exporter sans publier** ou sur **Publier**, en fonction de vos besoins.

   >[!NOTE]
   >
   >L’option **Publier** permet la publication immédiate du fragment d’expérience et l’envoie vers Target.

1. Appuyez/cliquez sur **OK** dans la boîte de dialogue de confirmation.

   Votre fragment d’expérience se trouve désormais dans Target.

   >[!NOTE]
   >
   >[Divers détails](/help/sites-authoring/experience-fragments.md#details-of-your-experience-fragment) sur l’exportation sont visibles dans le **mode Liste** de la console et dans **les Propriétés**.

   >[!NOTE]
   >
   >Lors de l’affichage d’un fragment d’expérience dans Adobe Target, la date de la *dernière modification* qui apparaît correspond à la dernière modification du fragment dans AEM. Il ne s’agit pas de la date de la dernière exportation du fragment vers Adobe Target.

>[!NOTE]
>
>Vous pouvez également procéder à l’exportation via l’éditeur de page, à l’aide des commandes comparables du menu [Informations sur la page](/help/sites-authoring/author-environment-tools.md#page-information).

## Utilisation des fragments d’expérience dans Adobe Target {#using-your-experience-fragments-in-adobe-target}

Après avoir effectué les tâches précédentes, le fragment d’expérience s’affiche sur la page Offres de Target. Consultez la [documentation spécifique de Target](https://experiencecloud.adobe.com/resources/help/en_US/target/target/aem-experience-fragments.html) pour en savoir plus sur ce qui est réalisable.

>[!NOTE]
>
>Lors de l’affichage d’un fragment d’expérience dans Adobe Target, la date de la *dernière modification* qui apparaît correspond à la dernière modification du fragment dans AEM. Il ne s’agit pas de la date de la dernière exportation du fragment vers Adobe Target.

## Suppression d’un fragment d’expérience déjà exporté vers Adobe Target {#deleting-an-experience-fragment-already-exported-to-adobe-target}

La suppression d’un fragment d’expérience qui a déjà été exporté vers Target peut entraîner des problèmes si le fragment est déjà utilisé pour une offre dans Target. L’offre ne serait alors plus utilisable, car c’est AEM qui fournit le contenu du fragment.

Pour éviter de tels problèmes :

* Si le fragment d’expérience n’est pas en cours d’utilisation par une activité, l’utilisateur peut le supprimer sans recevoir de message d’avertissement.
* Si le fragment d’expérience est en cours d’utilisation par une activité dans Target, un message d’erreur informe l’utilisateur d’AEM des risques que la suppression dudit fragment peut engendrer.

   Le message d’erreur apparu dans AEM n’empêche pas à l’utilisateur de forcer la suppression du fragment d’expérience. Si le fragment d’expérience est supprimé :

   * L’offre Target avec AEM fragment d’expérience peut présenter un comportement indésirable

      * L’offre sera probablement toujours rendue, car le HTML de fragment d’expérience a été envoyé à Target.
      * Les références contenues dans le fragment d’expérience peuvent ne pas fonctionner correctement si des ressources référencées ont également été supprimées dans AEM.
   * Bien sûr, toute modification supplémentaire apportée au fragment d’expérience est impossible, car le fragment d’expérience n’existe plus dans AEM.
