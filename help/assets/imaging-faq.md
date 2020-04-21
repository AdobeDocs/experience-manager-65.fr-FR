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
source-git-commit: 7daf89f7e69d3e2e938780ff98fd2df46723e708

---


# Imagerie dynamique {#smart-imaging}

## What is &quot;Smart Imaging&quot;? {#what-is-smart-imaging}

La technologie Smart Imaging exploite les fonctionnalités d’Adobe Sensei AI et travaille avec les paramètres d’image prédéfinis existants pour améliorer les performances des d’images en optimisant automatiquement le format, la taille et la qualité des images en fonction des capacités du navigateur client.

Smart Imaging bénéficie également de l’amélioration des performances grâce à l’intégration complète au meilleur service CDN d’Adobe. Ce service recherche la route Internet optimale entre les serveurs, réseaux et points d’appairage ; c’est-à-dire la route ayant une latence et/ou un taux de perte de paquets plus faibles que la route par défaut sur Internet.

Les exemples de ressources d’image suivants illustrent l’optimisation de l’imagerie intelligente ajoutée :

| Image<br>(URL) | Miniature   | Taille<br> (JPEG) | Taille (WebP)<br> (avec Smart Imaging) | % de réduction |
|---|---|---|---|---|
| [Image 1](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_6?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture1](/help/assets/assets-dm/picture1.png) | 73.75 Ko | 45.92 Ko | 38% |
| [Image 2](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_3?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture2](/help/assets/assets-dm/picture2.png) | 191 Ko | 70.66 Ko | 63% |
| [Image 3](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_2?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture3](/help/assets/assets-dm/picture3.png) | 96.64 Ko | 39.44 Ko | 59% |
| [Image 4](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_1?hei=500&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture4](/help/assets/assets-dm/picture4.png) | 315.80 Ko | 178.19 Ko | 44% |
|  |  |  |  | Moyenne = 51 % |

De la même manière que ci-dessus, Adobe a également effectué un test avec 7 009 URL provenant de sites clients en direct et a pu optimiser en moyenne 38 % la taille des fichiers JPEG et 31 % la taille des fichiers PNG au format WebP, grâce à la fonctionnalité d’imagerie intelligente.

## What are the key benefits of the latest Smart Imaging? {#what-are-the-key-benefits-of-smart-imaging}

Les images constituant la majorité du temps de chargement d’une page, l’amélioration des performances peut avoir un impact profond sur les indicateurs clés de performance de l’entreprise, tels qu’une conversion plus élevée, le temps passé sur le site et un taux de rebond plus faible sur le site.

Améliorations de la dernière version de Smart Imaging :

* Sert le contenu optimisé immédiatement (au moment de l’exécution).
* Utilise la technologie Adobe Sensei pour effectuer une conversion en fonction de la qualité (qlt) spécifiée dans la demande d’image.
* L’imagerie intelligente peut être désactivée à l’aide du paramètre d’URL &quot;bfc&quot;.
* TTL (Time To Live) indépendant. Auparavant, un TTL minimum de 12 heures était obligatoire pour que Smart Imaging fonctionne.
* Auparavant, les images d’origine et dérivées étaient mises en cache et il s’agissait d’un processus en 2 étapes pour invalider le cache. Dans la dernière version de Smart Imaging, seuls les dérivés sont mis en cache, ce qui permet un processus d’invalidation du cache en une seule étape.
* Les clients qui utilisent des en-têtes personnalisés dans leur jeu de règles (par exemple, &quot;Timing Allow &quot;, &quot;X-Robot&quot; comme suggéré dans [Ajout d’une valeur d’en-tête personnalisé aux réponses à l’image|Dynamic Media Classic](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/add-custom-header-val-image.html)) bénéficieront de la dernière version de l’imagerie dynamique, car ces en-têtes ne sont pas bloqués, contrairement à la version précédente de l’imagerie dynamique.

## L’imagerie dynamique entraîne-t-elle des frais de licence ? {#are-there-any-licensing-costs-associated-with-smart-imaging}

Non. Smart Imaging est inclus dans votre licence existante de Dynamic Media Classic (Scene7) ou d’AEM Dynamic Media (On Prem, AMS et AEM as a Cloud Service).

>[!NOTE]
>
>Smart Imaging n’est pas disponible pour les clients de Dynamic Media - Hybrid.


## Comment fonctionne l’imagerie dynamique ? {#how-does-smart-imaging-work}

Smart Imaging utilise Adobe Sensei pour convertir automatiquement les images au format, à la taille et à la qualité optimaux, en fonction des fonctionnalités du navigateur :

* Convertir automatiquement en WebP pour les navigateurs tels que Chrome, Firefox, Microsoft Edge, Android et Opera.
* Convertir automatiquement au format JPEG2000 pour les navigateurs tels que Safari.
* Convertir automatiquement au format JPEG pour les navigateurs tels qu’Internet Explorer 9+.
* Pour les navigateurs qui ne prennent pas en charge ces formats, le format d’image demandé à l’origine est diffusé.

Si la taille de l’image d’origine est inférieure à celle produite par Smart Imaging, l’image d’origine est diffusée.

## Quels sont les formats d’image pris en charge ?   {#what-image-formats-are-supported}

Les formats d’image suivants sont pris en charge pour Smart Imaging :
* JPEG
* PNG

<!-- For any other format mentioned in a URL, you should explicity turn off Smart Imaging.  Append modifier `bfc=off` to the URL for file formats other than JPEG and PNG. You can accomplish this by using either one of the following methods:

* Use a ruleset if the `fmt` modifier is mentioned in the URL. 
* Append in URL modifiers field of the presets concerned.

Adobe is working on a permanent fix that does not require you to append `bfc=off` for `fmt !=JPEG` or `fmt !=PNG`. This topic will be updated after the fix is delivered. -->

## How does Smart Imaging work with our existing image presets that are already in use? {#how-does-smart-imaging-work-with-our-existing-image-presets-that-are-already-in-use}

Smart Imaging fonctionne avec vos paramètres d’image prédéfinis existants et observe tous vos paramètres d’image, à l’exception de la qualité (qlt) et du format (fmt) si le format de fichier demandé est JPEG ou PNG. Pour la conversion de format, nous conservons la qualité vidéo totale, telle qu’elle est définie par vos paramètres d’image prédéfinis, mais avec une plus petite taille de fichier. Si la taille de l’image d’origine est inférieure à celle produite par Smart Imaging, l’image d’origine est diffusée.

<!-- In addition, if your image presets are used to return `fmt !=JPEG` or `fmt !=PNG`, be sure append `bfc=off` in the preset modifier field to return the requested file format. -->

## Will I have to change any URLs, image presets, or deploy any new code on my site for Smart Imaging? {#will-i-have-to-change-any-urls-image-presets-or-deploy-any-new-code-on-my-site-for-smart-imaging}

Non. L’imagerie dynamique fonctionne de manière transparente avec vos URL d’image et paramètres d’image prédéfinis existants. En outre, Smart Imaging n’exige pas que vous ajoutiez du code sur votre site Web pour détecter le navigateur d’un utilisateur. Tout ceci est géré automatiquement.

<!-- As mentioned earlier, Smart Imaging supports only JPEG and PNG image formats. For other formats, you need to append the `bfc=off` modifier to the URL as described earlier. -->

Also, see [Am I eligible to use Smart Imaging?](#am-i-eligible-to-use-smart-imaging) pour comprendre les conditions préalables requises pour l’imagerie intelligente.

## Smart Mmaging fonctionne-t-il avec HTTPS ? Et qu’en est-il du protocole HTTP/2 ?   {#does-smart-imaging-working-with-https-how-about-http}

Smart Imaging fonctionne avec les images diffusées via HTTP ou HTTPS. En outre, il fonctionne également sur HTTP/2.

## Puis-je utiliser l’imagerie dynamique ? {#am-i-eligible-to-use-smart-imaging}

Pour utiliser l’imagerie dynamique, votre  Contenu multimédia dynamique classique ou Contenu multimédia dynamique sur un compte AEM doit répondre aux exigences suivantes :

* Utiliser le réseau de diffusion de contenu (CDN) fourni par Adobe dans le cadre de votre licence.
* Utilisez un domaine dédié (par exemple, `images.company.com` ou `mycompany.scene7.com`), et non un domaine générique (par exemple, `s7d1.scene7.com`, `s7d2.scene7.com`ou `s7d13.scene7.com`).

Pour rechercher vos domaines, connectez-vous à votre (vos) compte(s) d’entreprise.

Appuyez sur **[!UICONTROL Configuration > Configuration de l’application > Paramètres généraux]**. Recherchez le champ intitulé **[!UICONTROL Nom du serveur publié]**. Si vous utilisez actuellement un domaine générique, vous pouvez demander de passer à votre propre domaine personnalisé dans le cadre de ce  lorsque vous envoyez un ticket d&#39;assistance technique.

Votre premier domaine personnalisé n’entraîne aucun coût supplémentaire avec une licence Contenu multimédia dynamique.

## What is the process for enabling Smart Imaging for my account? {#what-is-the-process-for-enabling-smart-imaging-for-my-account}

Vous devez envoyer la demande d’utilisation de l’imagerie dynamique ; elle n’est pas activée automatiquement.

1. Initiate a Technical Support request (email: `s7support@adobe.com`).
1. Indiquez les informations suivantes dans votre demande de support :

   1. Nom, adresse électronique et numéro de téléphone du contact principal.
   1. All domains to be enabled for smart imaging (that is, `images.company.com` or `mycompany.scene7.com`).

      Pour rechercher vos domaines, connectez-vous à votre (vos) compte(s) d’entreprise.

       Cliquez sur **[!UICONTROL Configuration > Configuration de l’application > Paramètres généraux]**.

      Recherchez le champ intitulé **[!UICONTROL Nom du serveur publié]**.
   1. Vérifiez que vous utilisez le CDN via Adobe et non le CDN géré avec une relation directe.
   1. Vérifiez que vous utilisez un domaine dédié, tel que `images.company.com` ou `mycompany.scene7.com`, et non un domaine générique, tel que `s7d1.scene7.com`, `s7d2.scene7.com` ou `s7d13.scene7.com`.

      Pour rechercher vos domaines, connectez-vous à votre (vos) compte(s) d’entreprise.

       Cliquez sur **[!UICONTROL Configuration > Configuration de l’application > Paramètres généraux]**.

      Recherchez le champ intitulé **[!UICONTROL Nom du serveur publié]**. Si vous utilisez actuellement un domaine Dynamic Media Classic générique, vous pouvez demander une migration vers votre domaine personnalisé dans le cadre de cette transition.
   1. Indiquez si vous avez également besoin de cette fonctionnalité pour fonctionner sur HTTP/2.

1. Le support technique vous ajoutera au d’attente client Smart Imaging en fonction de l’ordre dans lequel les demandes ont été envoyées.
1. Dès qu’Adobe est prêt à traiter votre demande, vous serez contacté par le support technique afin de programmer une date cible.
1. **Facultatif**: Vous avez la possibilité de tester l’imagerie intelligente dans le cadre de l’évaluation avant qu’Adobe ne mette la nouvelle fonctionnalité en production.
1. Une fois la procédure achevée, vous en serez informé par l’équipe de support.
1. Pour optimiser les performances de Smart Imaging, Adobe recommande de définir le paramètre Durée de vie (TTL) sur 24 heures ou plus. Ce paramètre définit la période pendant laquelle les ressources sont mises en cache par le réseau de diffusion de contenu. Pour modifier ce paramètre :

   1. Si vous utilisez Dynamic Media Classic, cliquez sur **[!UICONTROL Configuration > Configuration de l’application > Configuration de la publication > Serveur d’images]**. Définissez la valeur **[!UICONTROL Délai d’expiration par défaut du cache de client]** sur 24 ou plus.
   1. Si vous utilisez Contenu multimédia dynamique, suivez [ces instructions](config-dynamic.md). Set the **[!UICONTROL Expiration]** value 24 hours or longer.

## When can I expect my account to be enabled with Smart Imaging? {#when-can-i-expect-my-account-to-be-enabled-with-smart-imaging}

Les demandes sont traitées dans l’ordre dans lequel elles sont reçues par l’équipe du support technique, suivant la liste d’attente.

>[!NOTE]
Il peut y avoir un long délai, car l’activation de l’imagerie intelligente implique qu’Adobe efface le cache. Par conséquent, seul un petit nombre de transitions peuvent être traitées à la fois.

## What are the risks with switching over to use Smart Imaging? {#what-are-the-risks-with-switching-over-to-use-smart-imaging}

La page Web d’un client ne présente aucun risque. Sachez toutefois que le à l’imagerie dynamique efface votre cache sur le réseau de diffusion de contenu, car il implique de passer à une nouvelle configuration de Contenu multimédia dynamique classique ou Contenu multimédia dynamique sur AEM.

Au cours de la transition initiale, les images non mises en cache accèdent directement aux serveurs d’origine d’Adobe jusqu’à ce que le cache soit reconstitué. C’est pour cette raison qu’Adobe prévoit de ne gérer que quelques transitions à la fois afin d’offrir des performances acceptables lors de l’extraction des demandes de notre site d’origine. Pour la plupart des utilisateurs, le cache est entièrement reconstitué au niveau du réseau CDN sous 1 à 2 jours.

## Comment puis-je vérifier si l’imagerie dynamique fonctionne comme prévu ? {#how-can-i-verify-whether-smart-imaging-is-working-as-expected}

1. Une fois votre compte configuré avec l’imagerie dynamique, chargez une URL d’image Contenu multimédia dynamique classique (Scene7)/Contenu multimédia dynamique dans le navigateur.
1. Ouvrez le volet de Chrome pour les développeurs en cliquant sur **[!UICONTROL Afficher > Développeur > Outils de développement]** dans le navigateur. Vous pouvez également choisir n’importe quel outil de développement de navigateur de votre choix.

1. Assurez-vous que le cache est désactivé lorsque les outils de développement sont ouverts.

   * On Windows – navigate to settings in the developer tool pane, then select **[!UICONTROL Disable cache (while devtools is open)]** checkbox.
   * On Mac – in the developer pane, under the **[!UICONTROL Network]** tab, select **[!UICONTROL disable cache]** .

1. Observez que le type de contenu est converti au format approprié. La capture d’écran suivante montre une image PNG convertie dynamiquement en WebP sur Chrome.
1. Répétez ce test sur d’autres navigateurs et avec différentes conditions d’utilisation.

>[!NOTE]
Toutes les images ne sont pas converties. L’imagerie dynamique détermine si la conversion est nécessaire pour améliorer les performances. Dans certains cas, lorsqu’il n’y a pas de gain de performances attendu ou que le format n’est pas JPEG ou PNG, l’image n’est pas convertie.

![image2017-11-14_15398](assets/image2017-11-14_15398.png)

## L’imagerie intelligente peut-elle être désactivée pour une requête ? {#turning-off-smart-imaging}

Oui. Vous pouvez désactiver l’imagerie intelligente en ajoutant le modificateur `bfc=off` à l’URL.

## Quel &quot;réglage&quot; est disponible ? Existe-t-il des paramètres ou des comportements qui peuvent être définis ? (#tuning-settings)

Actuellement, vous pouvez éventuellement activer ou désactiver l’imagerie dynamique. Aucun autre réglage n&#39;est disponible.

## Si Smart Imaging gère les paramètres de qualité, y a-t-il des minimums et des maximums que nous pouvons définir ? Par exemple, est-il possible de définir &quot;pas inférieur à 60&quot; et &quot;pas supérieur à 80&quot; ? (#minimum-maximum)

Il n’existe aucune fonctionnalité de mise en service de ce type dans l’imagerie intelligente actuelle.

## Dans certains cas, une image JPEG est renvoyée dans Chrome au lieu d’une image WebP. Pourquoi cela arrive-t-il ? (#jpeg-webp)

L’imagerie dynamique détermine si la conversion est bénéfique ou non. Elle renvoie la nouvelle image uniquement si la conversion entraîne une taille de fichier plus petite avec une qualité comparable.
