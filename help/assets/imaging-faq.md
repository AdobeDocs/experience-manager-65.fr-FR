---
title: Imagerie dynamique
description: L’imagerie dynamique utilise les caractéristiques de visualisation uniques de chaque utilisateur pour diffuser automatiquement les images optimisées pour leur expérience, ce qui se traduit par des performances accrues et une meilleure interaction.
uuid: c11e52ba-8d64-4dc5-b30a-fc10c2b704e5
contentOwner: Rick Brough
topic-tags: dynamic-media
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
discoiquuid: bf8c6bbd-847d-43d7-9ff4-7231bfd8d107
translation-type: tm+mt
source-git-commit: b4b500cc80c6d498baaabe3a6863a3843b904f9b
workflow-type: tm+mt
source-wordcount: '2085'
ht-degree: 79%

---


# Imagerie dynamique {#smart-imaging}

## Qu’est-ce que l’imagerie dynamique ? {#what-is-smart-imaging}

Grâce aux fonctionnalités d’IA d’Adobe Sensei, la technologie d’imagerie dynamique traite les « paramètres d’image prédéfinis » existants pour améliorer les performances de la diffusion d’images en optimisant automatiquement le format, la taille et la qualité des images selon les possibilités du navigateur client.

L’imagerie dynamique tire également parti de sa parfaite intégration dans un service de réseau de diffusion de contenu haut de gamme proposé par Adobe afin d’offrir un gain de performance accru. Ce service recherche l’itinéraire Internet optimal entre les serveurs, réseaux et points d’appairage ; c’est-à-dire l’itinéraire ayant une latence et/ou un taux de perte de paquets plus faibles que l’itinéraire par défaut sur Internet.

Les exemples de ressources d’image suivants illustrent l’optimisation supplémentaire qu’apporte l’imagerie dynamique :

| Image<br>(URL) | Miniature | Taille<br> (JPEG) | Taille (WebP)<br> (avec imagerie dynamique) | % de réduction |
|---|---|---|---|---|
| [Image 1](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_6?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture1](/help/assets/assets-dm/picture1.png) | 73,75 Ko | 45,92 Ko | 38 % |
| [Image 2](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_3?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture2](/help/assets/assets-dm/picture2.png) | 191 Ko | 70,66 Ko | 63 % |
| [Image 3](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_2?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture3](/help/assets/assets-dm/picture3.png) | 96,64 Ko | 39,44 Ko | 59 % |
| [Image 4](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_1?hei=500&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture4](/help/assets/assets-dm/picture4.png) | 315,80 Ko | 178,19 Ko | 44 % |
|  |  |  |  | Moyenne = 51 % |

De la même manière que ci-dessus, Adobe a effectué un test avec 7 009 adresses URL provenant de sites clients actifs. L’imagerie dynamique a permis une optimisation supplémentaire moyenne de 38 % de la taille des fichiers JPEG et de 31 % pour les fichiers PNG au format WebP.

## Quels sont les principaux avantages de la plus récente technologie d’imagerie dynamique ? {#what-are-the-key-benefits-of-smart-imaging}

Les images sont les éléments qui demandent le plus de temps lors du chargement d’une page. Aussi, une amélioration des performances peut-elle avoir une incidence considérable sur les indicateurs IPC, tels qu’un taux de conversion plus élevé, une augmentation du temps passé sur le site et un taux de rebond moindre.

Améliorations apportées par la version la plus récente de l’imagerie dynamique :

* Diffusion immédiate de contenus optimisés (au moment de l’exécution).
* Mise en œuvre de la technologie Adobe Sensei pour effectuer la conversion en fonction de la qualité (qlt) spécifiée dans la demande d’image.
* Possibilité de désactiver l’imagerie dynamique à l’aide du paramètre d’URL « bfc ».
* Indépendance vis-à-vis du temps de vie (TTL). Auparavant, un TTL minimal de 12 heures était obligatoire pour le fonctionnement de l’imagerie dynamique.
* Auparavant également, les images d’origine et dérivées étaient mises en cache et un processus en deux étapes était nécessaire pour invalider le cache. Avec la technologie d’imagerie dynamique la plus récente, seules les images dérivées sont mises en cache, ce qui rend possible un processus d’invalidation du cache en une seule étape.
* Les clients qui utilisent des en-têtes personnalisés dans leurs jeux de règles (par exemple, « Timing-Allow-Origin », « X-Robot », comme suggéré dans la section [Ajout d’une valeur d’en-tête personnalisée aux réponses d’image | Dynamic Media Classic](https://helpx.adobe.com/fr/experience-manager/scene7/kb/base/scene7-rulesets/add-custom-header-val-image.html)) bénéficieront de la toute dernière version de l’imagerie dynamique, car ces en-têtes ne sont pas bloqués, contrairement à la version précédente.

## L’imagerie dynamique entraîne-t-elle des frais de licence ? {#are-there-any-licensing-costs-associated-with-smart-imaging}

Non. L’imagerie dynamique est incluse dans votre licence Dynamic Media Classic (Scene7) ou AEM Dynamic Media (on-premise, AMS et AEM as a Cloud Service).

>[!NOTE]
>
>L’imagerie dynamique n’est pas disponible pour les utilisateurs Dynamic Media – Hybrid.


## Comment fonctionne l’imagerie dynamique ? {#how-does-smart-imaging-work}

Lorsqu’une image est demandée par un consommateur, nous vérifions les caractéristiques de l’utilisateur et la convertissons au format d’image approprié en fonction du navigateur utilisé. Ces conversions de format sont effectuées de manière à ne pas dégrader la fidélité visuelle. L’imagerie intelligente convertit automatiquement les images dans différents formats en fonction des fonctionnalités du navigateur, comme suit.

* Convertir automatiquement en WebP pour les navigateurs suivants :
   * Chrome
   * Firefox
   * Microsoft Edge
   * Safari 14.0 +
      * Safari 14 uniquement avec iOS 14.0 et versions ultérieures et macOS BigSur et versions ultérieures
   * Android
   * Opera
* Prise en charge héritée du navigateur pour les éléments suivants :

   | Navigateur | Version du navigateur/du système d’exploitation | Format |
   | --- | --- | --- |
   | Safari | iOS 14.0 ou version antérieure | JPEG2000 |
   | Edge | 18 ou version antérieure | JPEGXR |
   | Internet Explorer | 9+ | JPEGXR |
* Pour les navigateurs qui ne prennent pas en charge ces formats, le format d’image demandé initialement est diffusé.

Si la taille de l’image d’origine est inférieure à celle produite par l’imagerie dynamique, l’image d’origine est diffusée.

## Quels sont les formats d’image pris en charge ?  {#what-image-formats-are-supported}

Les formats suivants sont pris en charge dans le cadre de l’imagerie dynamique :
* JPEG
* PNG

<!-- For any other format mentioned in a URL, you should explicity turn off Smart Imaging.  Append modifier `bfc=off` to the URL for file formats other than JPEG and PNG. You can accomplish this by using either one of the following methods:

* Use a ruleset if the `fmt` modifier is mentioned in the URL. 
* Append in URL modifiers field of the presets concerned.

Adobe is working on a permanent fix that does not require you to append `bfc=off` for `fmt !=JPEG` or `fmt !=PNG`. This topic will be updated after the fix is delivered. -->

## Comment l’imagerie dynamique fonctionne-t-elle avec les paramètres d’image prédéfinis qui sont déjà utilisés ? {#how-does-smart-imaging-work-with-our-existing-image-presets-that-are-already-in-use}

L’imagerie dynamique fonctionne avec vos paramètres d’image prédéfinis existants et conserve tous vos paramètres d’image, à l’exception de la qualité (qlt) et du format (fmt) si le format de fichier demandé est JPEG ou PNG. Pour la conversion de format, nous conservons la qualité vidéo totale, telle qu’elle est définie par vos paramètres d’image prédéfinis, mais avec une plus petite taille de fichier. Si la taille de l’image d’origine est inférieure à celle produite par l’imagerie dynamique, l’image d’origine est diffusée.

<!-- In addition, if your image presets are used to return `fmt !=JPEG` or `fmt !=PNG`, be sure append `bfc=off` in the preset modifier field to return the requested file format. -->

## Vais-je devoir modifier des URL ou des paramètres d’image prédéfinis, ou déployer du nouveau code sur mon site pour exploiter l’imagerie dynamique ? {#will-i-have-to-change-any-urls-image-presets-or-deploy-any-new-code-on-my-site-for-smart-imaging}

L’imagerie dynamique fonctionne en toute transparence avec vos URL d’image et paramètres d’image prédéfinis existants si vous configurez l’imagerie dynamique sur votre domaine personnalisé existant. En outre, l’imagerie dynamique n’exige pas que vous ajoutiez du code sur votre site web pour détecter le navigateur d’un utilisateur. Tout cela est géré automatiquement.

Si vous devez configurer un nouveau domaine personnalisé pour utiliser l’imagerie intelligente, les URL devront être mises à jour pour refléter ce domaine personnalisé.

Voir également [Suis-je autorisé à utiliser l’imagerie dynamique ?](#am-i-eligible-to-use-smart-imaging) pour connaître les conditions préalables requises pour l’imagerie dynamique.

<!-- No. Smart Imaging works seamlessly with your existing image URLs and image presets. In addition, Smart Imaging does not require you to add any code on your website to detect a user's browser. All of this is handled automatically. -->

<!-- As mentioned earlier, Smart Imaging supports only JPEG and PNG image formats. For other formats, you need to append the `bfc=off` modifier to the URL as described earlier. -->

## L’imagerie dynamique est-elle compatible avec le protocole HTTPS ? Et qu’en est-il du protocole HTTP/2 ?  {#does-smart-imaging-working-with-https-how-about-http}

L’imagerie dynamique fonctionne avec les images diffusées sur HTTP ou HTTPS. Elle fonctionne également sur HTTP/2.

## Puis-je utiliser l’imagerie dynamique ? {#am-i-eligible-to-use-smart-imaging}

Pour pouvoir utiliser l’imagerie dynamique, le compte Dynamic Media Classic ou Dynamic Media sur AEM de votre entreprise doit répondre aux conditions suivantes :

* Utiliser le réseau de diffusion de contenu (CDN) fourni par Adobe dans le cadre de votre licence.
* Utiliser un domaine dédié (par exemple, `images.company.com` ou `mycompany.scene7.com`), plutôt qu’un domaine générique (par exemple, `s7d1.scene7.com`, `s7d2.scene7.com` ou `s7d13.scene7.com`).

Pour rechercher vos domaines, connectez-vous à votre (vos) compte(s) d’entreprise.

Appuyez sur **[!UICONTROL Configuration > Configuration de l’application > Paramètres généraux.]** Recherchez le champ intitulé **[!UICONTROL Nom du serveur publié.]** Si vous utilisez actuellement un domaine générique, vous pouvez demander une migration vers votre domaine personnalisé dans le cadre de cette transition lorsque vous soumettez un ticket de support technique.

Votre premier domaine personnalisé n’entraîne aucun coût supplémentaire avec une licence Dynamic Media.

## Quelle est la marche à suivre afin d’activer l’imagerie dynamique pour mon compte ? {#what-is-the-process-for-enabling-smart-imaging-for-my-account}

Vous devez envoyer la demande d’utilisation de l’imagerie dynamique ; elle n’est pas activée automatiquement.

1. [Utilisez le Admin Console pour créer un dossier de support.](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html)
1. Fournissez les informations suivantes dans votre dossier de support :

   1. nom, adresse électronique et numéro de téléphone du contact principal.
   1. Tous les domaines à activer pour l’imagerie dynamique (c’est-à-dire `images.company.com` ou `mycompany.scene7.com`).

      Pour rechercher vos domaines, connectez-vous à votre (vos) compte(s) d’entreprise.

      Cliquez sur **[!UICONTROL Configuration > Configuration de l’application > Paramètres généraux.]**

      Recherchez le champ intitulé **[!UICONTROL Nom du serveur publié.]**
   1. Vérifiez que vous utilisez le CDN via Adobe et non le CDN géré avec une relation directe.
   1. Vérifiez que vous utilisez un domaine dédié, tel que `images.company.com` ou `mycompany.scene7.com`, et non un domaine générique, tel que `s7d1.scene7.com`, `s7d2.scene7.com` ou `s7d13.scene7.com`.

      Pour rechercher vos domaines, connectez-vous à votre (vos) compte(s) d’entreprise.

      Cliquez sur **[!UICONTROL Configuration > Configuration de l’application > Paramètres généraux.]**

      Recherchez le champ intitulé **[!UICONTROL Nom du serveur publié.]** Si vous utilisez actuellement un domaine Dynamic Media Classic générique, vous pouvez demander une migration vers votre domaine personnalisé dans le cadre de cette transition.
   1. Indiquez s’il doit également fonctionner sur HTTP/2.

1. Le support technique vous inscrira sur la liste d’attente des clients de l’imagerie dynamique en se basant sur l’ordre dans lequel les demandes ont été envoyées.
1. Dès qu’Adobe est prêt à traiter votre demande, vous serez contacté par le support technique afin de programmer une date cible.
1. **Facultatif** : vous avez la possibilité de tester l’imagerie dynamique dans le cadre de l’évaluation avant qu’Adobe ne mette la nouvelle fonctionnalité en production.
1. Une fois la procédure achevée, vous en serez informé par l’équipe de support.
1. Pour tirer pleinement parti des améliorations de performances de l’imagerie dynamique, Adobe recommande de définir le délai d’expiration (TTL) sur 24 heures ou plus. Ce paramètre définit la période pendant laquelle les ressources sont mises en cache par le réseau de diffusion de contenu. Pour modifier ce paramètre :

   1. Si vous utilisez Dynamic Media Classic, cliquez sur **[!UICONTROL Configuration > Configuration de l’application > Configuration de la publication > Serveur d’images.]** Définissez la valeur **[!UICONTROL Délai d’expiration par défaut du cache de client]** sur 24 ou plus.
   1. Si vous utilisez Dynamic Media, [procédez comme suit](config-dynamic.md). Définissez la valeur **[!UICONTROL Expiration]** sur 24 heures ou plus.

## Dans quel délai puis-je m’attendre à ce que l’imagerie dynamique soit activée pour mon compte ? {#when-can-i-expect-my-account-to-be-enabled-with-smart-imaging}

Les demandes sont traitées dans l’ordre de réception par l’équipe du support technique, suivant la liste d’attente.

>[!NOTE]
Le délai d’exécution peut être relativement long, car l’activation de l’imagerie dynamique implique qu’Adobe efface le cache. Seul un petit nombre de transitions peut donc être traité simultanément.

## Quels sont les risques liés au passage à l’imagerie dynamique ? {#what-are-the-risks-with-switching-over-to-use-smart-imaging}

La page web d’un client ne présente aucun risque. Cependant, vous devez savoir que le passage à l’imagerie dynamique efface votre cache sur le réseau de diffusion de contenu, car cela suppose une migration vers une nouvelle configuration de Dynamic Media Classic ou Dynamic Media sur AEM.

Au cours de la transition initiale, les images non mises en cache accèdent directement aux serveurs d’origine d’Adobe jusqu’à ce que le cache soit reconstitué. C’est pour cette raison qu’Adobe prévoit de ne gérer que quelques transitions à la fois afin d’offrir des performances acceptables lors de l’extraction des demandes de notre site d’origine. Pour la plupart des utilisateurs, le cache est entièrement reconstitué au niveau du réseau CDN sous 1 à 2 jours.

## Comment puis-je vérifier si l’imagerie dynamique fonctionne comme prévu ? {#how-can-i-verify-whether-smart-imaging-is-working-as-expected}

1. Une fois que l’imagerie dynamique est activée sur votre compte, chargez une URL d’image Dynamic Media Classic (Scene7)/Dynamic Media sur le navigateur.
1. Ouvrez le volet de Chrome pour les développeurs en cliquant sur **[!UICONTROL Afficher > Développeur > Outils de développement]** dans le navigateur. Vous pouvez également sélectionner l’outil de développement de navigateur de votre choix.

1. Assurez-vous que le cache est désactivé lorsque les outils de développement sont ouverts.

   * Sous Windows, accédez aux paramètres dans le volet de l’outil de développement, puis cochez la case **[!UICONTROL Désactiver le cache (lorsque les outils de développement sont ouverts)]**.
   * Sous Mac, dans le volet Développeur, sous l’onglet **[!UICONTROL Réseau]**, sélectionnez **[!UICONTROL désactiver le cache]**.

1. Observez que le type de contenu est converti au format approprié. L’écran ci-dessous illustre la conversion dynamique d’une image PNG au format WebP sur Chrome.
1. Répétez ce test sur d’autres navigateurs et avec différentes conditions d’utilisation.

>[!NOTE]
Toutes les images ne sont pas converties. L’imagerie dynamique détermine si la conversion est requise en vue d’améliorer les performances. Dans certains cas, si aucune amélioration des performances n’est attendue, ou que le format n’est pas JPEG ou PNG, l’image n’est pas convertie.

![image2017-11-14_15398](assets/image2017-11-14_15398.png)

## Comment puis-je connaître le gain de performance ? Y a-t-il un moyen de noter les avantages de Smart Imaging ? {#performance-gain}

**A propos des en-têtes Smart Imaging**

Les valeurs d’en-tête Smart Imaging ne fonctionnent que lorsque des requêtes non mises en cache sont diffusées à compter de maintenant. Cela permet de maintenir la compatibilité du cache actuel et d’éviter d’avoir à effectuer des calculs lorsque les images sont diffusées par le biais du cache.

Pour utiliser des en-têtes d’imagerie intelligente, vous devez ajouter le`cache=off`modificateur à vos requêtes. Voir[Cache dans l’API](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-is-http-cache.html)de diffusion et de rendu des images de Contenu multimédia dynamique.

Exemple d’utilisation `cache=off` (à des fins d’illustration uniquement) :

`https://domain.scene7.com/is/image/companyName/imageName?cache=off` 

Après avoir utilisé une telle requête, dans la section En-têtes de réponse, vous pouvez voir `-x-adobe-smart-imaging` l’en-tête. Reportez-vous à la capture d&#39;écran suivante avec `-x-adobe-smart-imaging` mise en évidence.

![smart-imaging-header](/help/assets/assets-dm/smart-imaging-header2.png) 

Cette valeur d’en-tête indique ce qui suit :

* Smart Imaging travaille pour la société.
* La valeur positive (>=0) indique que la conversion a réussi. Dans ce cas, une nouvelle image (webP ici) est renvoyée.
* La valeur négative (&lt;0) indique que la conversion a échoué. Dans ce cas, l’image d’origine demandée est renvoyée (JPEG par défaut, si elle n’est pas spécifiée).
* La valeur indique la différence en octets entre l’image demandée et la nouvelle image. Dans ce cas, les octets enregistrés sont de 75048, soit environ 75 Ko pour une image. 
   * La valeur négative indique que l’image demandée est plus petite que la nouvelle image. La différence de taille est négative, mais l&#39;image diffusée est l&#39;image demandée d&#39;origine uniquement

**Quand utiliser les en-têtes d&#39;imagerie intelligente ?**

Les en-têtes de réponse Smart Imaging sont activés à des fins de débogage ou tout en mettant en évidence les avantages de Smart Imaging uniquement. L’utilisation`cache=off`dans des scénarios normaux peut avoir un impact significatif sur les temps de charge.

## Est-il possible de désactiver l’imagerie dynamique quelle que soit la raison ? {#turning-off-smart-imaging}

Oui. Vous pouvez désactiver l’imagerie dynamique en ajoutant le modificateur `bfc=off` à l’URL.

## Quel « réglage » est disponible ? Existe-t-il des paramètres ou des comportements pouvant être définis ? (#tuning-settings)

Actuellement, vous pouvez éventuellement activer ou désactiver l’imagerie dynamique. Aucun autre réglage n’est disponible.

## Si l’imagerie dynamique gère les paramètres de qualité, existe-t-il des valeurs minimales et maximales que nous pouvons définir ? Par exemple, est-il possible de définir une qualité « non inférieure à 60 » et « non supérieure à 80 » ? (#minimum-maximum)

Il n’existe aucune fonctionnalité de configuration de ce type dans la technologie actuelle d’imagerie dynamique.

## Dans certains cas, c’est une image JPEG qui est renvoyée au navigateur Chrome au lieu d’une image WebP. Pourquoi cela arrive-t-il ? (#jpeg-webp)

L’imagerie dynamique détermine si la conversion apporte ou non un bénéfice. Elle ne renvoie la nouvelle image que si la conversion parvient à réduire la taille du fichier avec une qualité comparable.
