---
title: Imagerie dynamique
description: L’imagerie intelligente applique les caractéristiques d’affichage uniques de chaque utilisateur afin de fournir automatiquement les images appropriées optimisées pour leur expérience, ce qui se traduit par de meilleures performances et un meilleur engagement.
uuid: c11e52ba-8d64-4dc5-b30a-fc10c2b704e5
contentOwner: Rick Brough
topic-tags: dynamic-media
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
discoiquuid: bf8c6bbd-847d-43d7-9ff4-7231bfd8d107
feature: Asset Management
role: Business Practitioner, Administrator
exl-id: e427d4ee-d5c8-421b-9739-f3cf2de36e41
translation-type: tm+mt
source-git-commit: 8d27457ad88cb84e670e78bab4c40da36fcfc629
workflow-type: tm+mt
source-wordcount: '1912'
ht-degree: 50%

---


# Imagerie dynamique {#smart-imaging}

## Qu’est-ce que l’imagerie dynamique ? {#what-is-smart-imaging}

La technologie Smart Imaging applique les fonctionnalités d’IA Adobe Sensei et fonctionne avec les &quot;paramètres d’image prédéfinis&quot; existants pour améliorer les performances de la diffusion d’images en optimisant automatiquement le format, la taille et la qualité des images en fonction des fonctionnalités du navigateur client.

>[!NOTE]
>
>Cette fonctionnalité requiert que vous utilisiez le CDN (Content Diffusion Network) prêt à l’emploi fourni avec Adobe Experience Manager Dynamic Media. Aucun autre CDN personnalisé n’est pris en charge avec cette fonctionnalité.

L’imagerie dynamique tire également parti de sa parfaite intégration dans un service de réseau de diffusion de contenu haut de gamme proposé par Adobe afin d’offrir un gain de performance accru. Ce service trouve la route Internet optimale entre les serveurs, les réseaux et les points d’écoute. Il trouve un itinéraire présentant la latence la plus faible et le taux de perte de paquets le plus faible au lieu d&#39;utiliser l&#39;itinéraire par défaut sur Internet.

Les exemples de ressources d’image suivants illustrent l’optimisation supplémentaire qu’apporte l’imagerie dynamique :

| Image<br>(URL) | Miniature | Taille<br> (JPEG) | Taille (WebP)<br> (avec imagerie dynamique) | % de réduction |
|---|---|---|---|---|
| [Image 1](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_6?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture1](/help/assets/assets-dm/picture1.png) | 73,75 Ko | 45,92 Ko | 38 % |
| [Image 2](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_3?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture2](/help/assets/assets-dm/picture2.png) | 191 Ko | 70,66 Ko | 63 % |
| [Image 3](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_2?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture3](/help/assets/assets-dm/picture3.png) | 96,64 Ko | 39,44 Ko | 59 % |
| [Image 4](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_1?hei=500&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture4](/help/assets/assets-dm/picture4.png) | 315,80 Ko | 178,19 Ko | 44 % |
|  |  |  |  | Moyenne = 51 % |

De la même manière que ci-dessus, l’Adobe a également exécuté un test avec 7 009 URL provenant de sites clients actifs. Ils ont pu obtenir en moyenne 38 % d’optimisation supplémentaire de la taille de fichier pour le format JPEG. Pour les fichiers PNG au format WebP, ils ont été en mesure d’optimiser en moyenne 31 % de la taille de fichier supplémentaire. Ce type d&#39;optimisation est possible grâce à la fonctionnalité d&#39;imagerie intelligente.

## Quels sont les principaux avantages de la plus récente technologie d’imagerie dynamique ? {#what-are-the-key-benefits-of-smart-imaging}

Les images constituant la majeure partie du temps de chargement d’une page, l’amélioration des performances peut avoir un impact profond sur une activité, notamment une conversion plus élevée, la durée de consultation du site et un taux de rebonds du site plus faible.

Améliorations apportées par la version la plus récente de l’imagerie dynamique :

* Amélioration du classement d’optimisation du référencement de Google pour les pages Web à l’aide de la dernière version d’Smart Imaging.
* Diffusion immédiate de contenus optimisés (au moment de l’exécution).
* Mise en œuvre de la technologie Adobe Sensei pour effectuer la conversion en fonction de la qualité (qlt) spécifiée dans la demande d’image.
* Possibilité de désactiver l’imagerie dynamique à l’aide du paramètre d’URL « bfc ».
* Indépendance vis-à-vis du temps de vie (TTL). Auparavant, un TTL minimal de 12 heures était obligatoire pour le fonctionnement de l’imagerie dynamique.
* Auparavant, les images d’origine et dérivées étaient mises en cache et il s’agissait d’un processus en deux étapes pour invalider le cache. Dans la dernière version de Smart Imaging, seuls les dérivés sont mis en cache, ce qui permet un processus d’invalidation en une seule étape du cache.
* Les clients qui utilisent des en-têtes personnalisés dans leur ensemble de règles bénéficient de la dernière version de Smart Imaging, car ces en-têtes ne sont pas bloqués, contrairement à la version précédente de Smart Imaging. Par exemple, &quot;Timing Allow Origine&quot;, &quot;X-Robot&quot; comme suggéré dans [Ajouter une valeur d&#39;en-tête personnalisée aux réponses d&#39;image|Dynamic Media Classic](https://helpx.adobe.com/fr/experience-manager/scene7/kb/base/scene7-rulesets/add-custom-header-val-image.html).

## L’imagerie dynamique entraîne-t-elle des frais de licence ? {#are-there-any-licensing-costs-associated-with-smart-imaging}

Non. Smart Imaging est inclus avec votre licence existante de Dynamic Media Classic ou Adobe Experience Manager - Dynamic Media (On-prem, AMS et Adobe Experience Manager en tant que Cloud Service).

>[!NOTE]
>
>Smart Imaging n’est pas disponible pour les clients Dynamic Media - Hybrid.

## Comment fonctionne l’imagerie dynamique ? {#how-does-smart-imaging-work}

Lorsqu’une image est demandée par un utilisateur, Smart Imaging vérifie les caractéristiques de l’utilisateur et la convertit au format d’image approprié en fonction du navigateur utilisé. Ces conversions de format s’effectuent de manière à garantir une représentation fidèle. L’imagerie dynamique convertit automatiquement les images dans différents formats en fonction des capacités du navigateur de la manière suivante.

<!--   * Safari 14.0 +
    * Safari 14 only with iOS 14.0 and above and macOS BigSur and above -->

* Convertir automatiquement vers WebP pour les navigateurs suivants :
   * Chrome
   * Firefox
   * Microsoft® Edge
   * Safari (sur iOS, macOS, iPadOS), pourvu que le navigateur et la version du système d’exploitation prennent en charge WebP
   * Android™
   * Opera
* Prise en charge des navigateurs existants pour les éléments suivants :

   | Navigateur | Version du navigateur/du système d’exploitation | Format |
   | --- | --- | --- |
   | Safari | Version antérieure à iOS/iPad 14.0 ou macOS BigSur | JPEG2000 |
   | Edge | Avant 18 | JPEGXR |
   | Internet Explorer | 9+ | JPEGXR |
* Pour les navigateurs qui ne prennent pas en charge ces formats, le format d’image demandé initialement est diffusé.

Si la taille de l’image d’origine est inférieure à celle produite par l’imagerie dynamique, l’image d’origine est diffusée.

## Quels sont les formats d’image pris en charge ? {#what-image-formats-are-supported}

Les formats suivants sont pris en charge dans le cadre de l’imagerie dynamique :

* JPEG
* PNG

<!-- CQDOC-15846 For any other format mentioned in a URL, you should explicity turn off Smart Imaging.  Append modifier `bfc=off` to the URL for file formats other than JPEG and PNG. You can accomplish this by using either one of the following methods:

* Use a ruleset if the `fmt` modifier is mentioned in the URL. 
* Append in URL modifiers field of the presets concerned.

Adobe is working on a permanent fix that does not require you to append `bfc=off` for `fmt !=JPEG` or `fmt !=PNG`. This topic will be updated after the fix is delivered. -->

## Comment l’imagerie intelligente fonctionne-t-elle avec mes paramètres d’image prédéfinis existants déjà utilisés ? {#how-does-smart-imaging-work-with-our-existing-image-presets-that-are-already-in-use}

Smart Imaging fonctionne avec vos paramètres d’image prédéfinis existants et observe tous vos paramètres d’image, à l’exception de la qualité (`qlt`) et du format (`fmt`) si le format de fichier demandé est JPEG ou PNG. Pour la conversion de format, Smart Imaging conserve une fidélité visuelle complète, telle que définie par vos paramètres d’image prédéfinis, mais à une taille de fichier inférieure. Si la taille de l’image d’origine est inférieure à celle produite par l’imagerie dynamique, l’image d’origine est diffusée.

<!-- CQDOC-15846 In addition, if your image presets are used to return `fmt !=JPEG` or `fmt !=PNG`, be sure append `bfc=off` in the preset modifier field to return the requested file format. -->

## Dois-je modifier des URL, des paramètres d’image prédéfinis ou déployer un nouveau code sur mon site pour l’imagerie intelligente ? {#will-i-have-to-change-any-urls-image-presets-or-deploy-any-new-code-on-my-site-for-smart-imaging}

L’imagerie dynamique fonctionne en toute transparence avec les URL et les paramètres prédéfinis des images existantes si vous configurez l’imagerie dynamique sur votre domaine personnalisé existant. En outre, l’imagerie dynamique n’exige pas que vous ajoutiez du code sur votre site web pour détecter le navigateur d’un utilisateur. Tout est géré automatiquement.

Si vous devez configurer un nouveau domaine personnalisé pour utiliser l’imagerie intelligente, les URL doivent être mises à jour pour refléter ce domaine personnalisé.

Pour comprendre les conditions préalables requises pour l&#39;imagerie intelligente, voir [Suis-je éligible pour l&#39;utilisation de l&#39;imagerie intelligente ?](#am-i-eligible-to-use-smart-imaging)

<!-- No. Smart Imaging works seamlessly with your existing image URLs and image presets. In addition, Smart Imaging does not require you to add any code on your website to detect a user's browser. All of this is handled automatically. -->

<!-- As mentioned earlier, Smart Imaging supports only JPEG and PNG image formats. For other formats, you need to append the `bfc=off` modifier to the URL as described earlier. -->

## L’imagerie dynamique est-elle compatible avec le protocole HTTPS ? Et qu’en est-il du protocole HTTP/2 ?  {#does-smart-imaging-working-with-https-how-about-http}

L’imagerie dynamique fonctionne avec les images diffusées sur HTTP ou HTTPS. Elle fonctionne également sur HTTP/2.

## Puis-je utiliser l’imagerie dynamique ? {#am-i-eligible-to-use-smart-imaging}

Pour utiliser Smart Imaging, votre société Dynamic Media Classic ou Dynamic Media sur compte Experience Manager doit répondre aux exigences suivantes :

* Utiliser le réseau de diffusion de contenu (CDN) fourni par Adobe dans le cadre de votre licence.
* Utiliser un domaine dédié (par exemple, `images.company.com` ou `mycompany.scene7.com`), plutôt qu’un domaine générique (par exemple, `s7d1.scene7.com`, `s7d2.scene7.com` ou `s7d13.scene7.com`).

Pour rechercher vos domaines, ouvrez l&#39;[application de bureau Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html?lang=fr#getting-started), puis connectez-vous à votre ou vos comptes de société.

Appuyez sur **[!UICONTROL Configuration > Configuration de l’application > Paramètres généraux]**. Recherchez le champ intitulé **[!UICONTROL Nom du serveur publié]**. Si vous utilisez actuellement un domaine générique, vous pouvez demander une migration vers votre domaine personnalisé dans le cadre de cette transition lorsque vous soumettez un ticket de support technique.

Votre premier domaine personnalisé n’entraîne aucun coût supplémentaire avec une licence Dynamic Media.

## Quelle est la marche à suivre afin d’activer l’imagerie dynamique pour mon compte ? {#what-is-the-process-for-enabling-smart-imaging-for-my-account}

Vous lancez une demande d’utilisation de l’imagerie intelligente ; elle n&#39;est pas activée automatiquement.

1. [Utilisez Admin Console pour créer un dossier d’assistance.](https://helpx.adobe.com/fr/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html)
1. Indiquez les informations suivantes dans votre dossier d’assistance :

   1. nom, adresse électronique et numéro de téléphone du contact principal.
   1. Tous les domaines à activer pour l’imagerie dynamique (c’est-à-dire `images.company.com` ou `mycompany.scene7.com`).

      Pour rechercher vos domaines, ouvrez l&#39;[application de bureau Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), puis connectez-vous à votre ou vos comptes de société.

      Cliquez sur **[!UICONTROL Configuration > Configuration de l’application > Paramètres généraux]**.

      Recherchez le champ intitulé **[!UICONTROL Nom du serveur publié.]**
   1. Vérifiez que vous utilisez le CDN via Adobe et non le CDN géré avec une relation directe.
   1. Vérifiez que vous utilisez un domaine dédié, tel que `images.company.com` ou `mycompany.scene7.com`, et non un domaine générique, tel que `s7d1.scene7.com`, `s7d2.scene7.com` ou `s7d13.scene7.com`.

      Pour rechercher vos domaines, ouvrez l&#39;[application de bureau Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), puis connectez-vous à votre ou vos comptes de société.

      Cliquez sur **[!UICONTROL Configuration > Configuration de l’application > Paramètres généraux]**.

      Recherchez le champ intitulé **[!UICONTROL Nom du serveur publié]**. Si vous utilisez actuellement un domaine Dynamic Media Classic générique, vous pouvez demander une migration vers votre domaine personnalisé dans le cadre de cette transition.
   1. Indiquez si vous devez également utiliser Smart Imaging sur HTTP/2.

1. Le service à la clientèle d’Adobe vous ajoute à la Liste d’attente du client Smart Imaging en fonction de l’ordre dans lequel les demandes ont été envoyées.
1. Lorsque l’Adobe est prêt à traiter votre demande, le service d’assistance vous contacte pour coordonner et définir une date de cible.
1. **Facultatif** : Vous pouvez également tester l’imagerie intelligente dans le cadre de l’évaluation avant que l’Adobe ne pousse la nouvelle fonction en production.
1. Vous êtes averti après l’exécution par le service à la clientèle.
1. Pour tirer pleinement parti des améliorations de performances de l’imagerie dynamique, Adobe recommande de définir le délai d’expiration (TTL) sur 24 heures ou plus. Ce paramètre définit la période pendant laquelle les ressources sont mises en cache par le réseau de diffusion de contenu. Pour modifier ce paramètre :

   1. Si vous utilisez Dynamic Media Classic, cliquez sur **[!UICONTROL Configuration > Configuration de l’application > Configuration de la publication > Serveur d’images]**. Définissez la valeur **[!UICONTROL Délai d’expiration par défaut du cache de client]** sur 24 ou plus.
   1. Si vous utilisez Dynamic Media, [procédez comme suit](config-dynamic.md). Définissez la valeur **[!UICONTROL Expiration]** sur 24 heures ou plus.

## Dans quel délai puis-je m’attendre à ce que l’imagerie dynamique soit activée pour mon compte ? {#when-can-i-expect-my-account-to-be-enabled-with-smart-imaging}

Les demandes sont traitées dans l’ordre dans lequel elles sont reçues par le service à la clientèle, selon la Liste d’attente.

>[!NOTE]
>
>Il peut y avoir un long délai, car l’activation de l’imagerie intelligente implique l’effacement du cache par Adobe. Seul un petit nombre de transitions peut donc être traité simultanément.

## Quels sont les risques liés au passage à l’imagerie dynamique ? {#what-are-the-risks-with-switching-over-to-use-smart-imaging}

La page web d’un client ne présente aucun risque. Cependant, la transition de Smart Imaging efface votre cache sur le réseau de diffusion de contenu car elle implique de passer à une nouvelle configuration de Dynamic Media Classic ou Dynamic Media sur Experience Manager.

Au cours de la transition initiale, les images non mises en cache ont directement atteint les serveurs d’origine du Adobe jusqu’à ce que le cache soit reconstitué. Par conséquent, l’Adobe prévoit de gérer quelques transitions client à la fois afin de maintenir des performances acceptables lors de l’extraction des demandes de l’origine. Pour la plupart des clients, le cache est entièrement reconstitué sur le réseau de diffusion de contenu dans un délai d’environ 1 à 2 jours.

## Comment puis-je vérifier si l’imagerie dynamique fonctionne comme prévu ? {#how-can-i-verify-whether-smart-imaging-is-working-as-expected}

1. Une fois votre compte configuré avec l’imagerie intelligente, chargez une URL d’image Dynamic Media Classic ou Adobe Experience Manager - Dynamic Media sur le navigateur.
1. Ouvrez le volet de Chrome pour les développeurs en cliquant sur **[!UICONTROL Afficher > Développeur > Outils de développement]** dans le navigateur. Vous pouvez également sélectionner l’outil de développement de navigateur de votre choix.

1. Assurez-vous que le cache est désactivé lorsque les outils de développement sont ouverts.

   * Sous Windows®, accédez aux paramètres du volet d’outils du développeur, puis cochez la case **[!UICONTROL Désactiver le cache (alors que devtools est ouvert)]**.
   * Sur macOS, dans le volet développeur, sous l’onglet **[!UICONTROL Réseau]**, sélectionnez **[!UICONTROL désactiver le cache]**.

1. Observez que le type de contenu est converti au format approprié. L’écran ci-dessous illustre la conversion dynamique d’une image PNG au format WebP sur Chrome.
1. Répétez ce test sur d’autres navigateurs et avec différentes conditions d’utilisation.

>[!NOTE]
>
>Toutes les images ne sont pas converties. Smart Imaging décide si la conversion peut améliorer les performances. Parfois, lorsque les performances ne sont pas améliorées ou que le format n’est pas JPEG ou PNG, l’image n’est pas convertie.

![image2017-11-14_15398](assets/image2017-11-14_15398.png)

## Est-il possible de désactiver l’imagerie dynamique quelle que soit la raison ? {#turning-off-smart-imaging}

Oui. Vous pouvez désactiver l’imagerie dynamique en ajoutant le modificateur `bfc=off` à l’URL.

## Quel « réglage » est disponible ? Existe-t-il des paramètres ou des comportements pouvant être définis ? (#tuning-settings)

Actuellement, vous pouvez éventuellement activer ou désactiver l’imagerie dynamique. Aucun autre réglage n’est disponible.

## Si Smart Imaging gère les paramètres de qualité, existe-t-il des minimums et des maximums à définir ? Par exemple, est-il possible de définir une qualité « non inférieure à 60 » et « non supérieure à 80 » ? (#minimum-maximum)

Il n’existe aucune fonctionnalité de configuration de ce type dans la technologie actuelle d’imagerie dynamique.

## Il arrive qu’une image JPEG soit renvoyée dans Chrome au lieu d’une image WebP. Pourquoi ? (#jpeg-webp)

L’imagerie dynamique détermine si la conversion apporte ou non un bénéfice. Elle ne renvoie la nouvelle image que si la conversion parvient à réduire la taille du fichier avec une qualité comparable.
