---
title: Principales fonctionnalités et améliorations cumulées dans la version 6.5 d’Adobe Experience Manager.
description: Liste cumulée des fonctionnalités et améliorations clés apportées à Adobe Experience Manager 6.5 à partir des huit versions précédentes du pack de services.
content-type: reference
docset: aem65
feature: Release Information
role: User,Admin,Architect,Developer
exl-id: 01fe5b53-2244-445f-a4d0-bd58ea38b611
solution: Experience Manager
source-git-commit: 10268f617b8a1bb22f1f131cfd88236e7d5beb47
workflow-type: tm+mt
source-wordcount: '2334'
ht-degree: 100%

---

# Principales fonctionnalités et améliorations cumulées

Liste cumulée des fonctionnalités et améliorations clés d’Adobe Experience Manager 6.5 pour les huit versions précédentes du pack de services.

Voir également les [Notes de mise à jour du dernier pack de services d’Adobe Experience Manager 6.5](/help/release-notes/release-notes.md)

## AEM 6.5, Pack de services 18—7 décembre, 2023

* Activation de la personne Éditeur de page/Composant d’image Sites pour référencer des ressources à partir du service cloud Assets à distance. (SITES-13448, SITES-13433)
* AEM prend désormais en charge le tri côté serveur pour accélérer la navigation du projet en vue Liste. Les nœuds de projet sont triés en fonction de la colonne sélectionnée par l’utilisateur ou l’utilisatrice avant d’apparaître dans l’interface.

### [!DNL Forms]

* **Nouveaux composants principaux de formulaires adaptatifs** : des onglets verticaux, des conditions générales et une case à cocher sont ajoutés pour améliorer l’évolutivité des formulaires.
   * **[Composant de case à cocher](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/checkbox.html?lang=fr)** : les formulaires adaptatifs basés sur les composants principaux peuvent désormais inclure un composant de case à cocher. Il permet aux utilisateurs et utilisatrices de faire des choix binaires, en sélectionnant ou en désélectionnant une option particulière. Il s’affiche généralement sous la forme d’une petite case sur laquelle vous pouvez cliquer ou appuyer pour basculer entre deux états : cochée et décochée. La case à cocher est un élément de formulaire courant, utilisé pour présenter un choix oui/non ou vrai/faux.

   * **[Composant Conditions générales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/terms-and-conditions.html?lang=fr)** : les formulaires adaptatifs basés sur les composants principaux peuvent désormais inclure un composant Conditions générales. Il permet aux personnes créant les formulaires d’introduire une section spécifique dans le formulaire, dans laquelle les utilisateurs et utilisatrices peuvent consulter les conditions générales ou les accords juridiques associés à l’utilisation d’un service, d’un produit ou d’une plateforme. Ce composant est conçu pour informer les utilisateurs et utilisatrices des règles, des réglementations et des obligations qu’ils acceptent en envoyant le formulaire.

     ![Composants Onglets verticaux, Conditions générales et Case à cocher](/help/forms/using/assets/forms-components.png)

   * **[Composant Onglets verticaux](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/vertical-tabs.html?lang=fr)** : les formulaires adaptatifs basés sur les composants principaux peuvent désormais organiser le contenu des formulaires en une liste verticale d’onglets, ce qui assure une disposition structurée et navigable. L’utilisation d’onglets verticaux dans un formulaire peut améliorer l’expérience globale de l’utilisateur ou de l’utilisatrice en simplifiant la navigation et en améliorant l’organisation du contenu du formulaire, en particulier lorsqu’un formulaire contient plusieurs sections ou des informations complexes.

* **[Version 64 bits d’AEM Forms Designer](/help/forms/using/installing-configuring-designer.md)** : la version 64 bits d’AEM Forms Designer offre des performances, une évolutivité et une gestion de la mémoire améliorées pour optimiser votre expérience de création de formulaires. Grâce à l’architecture 64 bits, vous pouvez aborder facilement des projets plus volumineux et plus complexes, assurant ainsi des workflows de conception transparents et une efficacité optimisée. Améliorez encore vos capacités de conception de formulaire et accueillez l’avenir d’AEM Forms Designer avec cette version de pointe.

* **[Connexion d’un formulaire adaptatif à une liste Microsoft® SharePoint](/help/forms/using/configuring-submit-actions.md#submit-to-microsoft&reg;-sharepoint-list)** : AEM Forms assure une intégration prête à l’emploi pour envoyer les données de formulaire directement à la liste SharePoint, ce qui vous permet d’utiliser les fonctionnalités des listes SharePoint. Vous pouvez configurer une liste Microsoft® SharePoint comme source de données pour un modèle de données de formulaire et utiliser l’action Envoyer à l’aide du modèle de données de formulaire pour connecter un formulaire adaptatif à la liste SharePoint.

* **[Prise en charge de la configuration des propriétés de document d’enregistrement pour les fragments de formulaire adaptatif](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md)** : vous pouvez désormais personnaliser facilement vos fragments de formulaire adaptatif et ses champs dans l’éditeur de formulaire adaptatif.

* **XMLFM 64 bits** : l’itération 64 bits de XMLFM améliore les performances, l’évolutivité et la gestion de la mémoire. Il s’agit du premier service natif 64 bits déployé côté serveur. En exploitant sa capacité intrinsèque à accéder à des ressources de mémoire plus importantes par rapport à son équivalent 32 bits, XMLFM 64 bits permet une gestion transparente des charges de travail de rendu plus lourdes. Ce jalon représente non seulement un bond en avant en termes de performances, mais il introduit également des améliorations clés du framework de service natif dans le serveur AEM Forms. Cette mise à jour permet au serveur AEM Forms de prendre en charge n’importe quel service natif 64 bits en toute transparence.

## AEM 6.5, Pack de services 18—24 août, 2023

* Assets, Dynamic Media - [Prise en charge du suivi de sous-titres et d’audio multiples pour les vidéos dans Dynamic Media](/help/assets/video.md#about-msma) : vous pouvez désormais facilement ajouter plusieurs sous-titres et plusieurs pistes audio à une vidéo principale. Cette fonctionnalité signifie que vos vidéos sont accessibles à une audience mondiale. Vous pouvez personnaliser une seule vidéo principale publiée pour une audience mondiale dans plusieurs langues et respecter les directives d’accessibilité pour différentes régions géographiques. Les auteurs et autrices peuvent également gérer les sous-titres et les pistes audio à partir d’un seul onglet de l’interface utilisateur.
* Ressources - À partir des résultats de recherche, vous pouvez désormais accéder à l’emplacement du dossier contenant une ressource, ce qui vous permet d’effectuer diverses tâches de gestion des ressources numériques.
* Les performances du sélecteur Polaris de sites dans les fragments de contenu ont été améliorées.
* La personne utilisant l’éditeur de pages/le composant d’images des sites peut référencer des actifs à partir du service cloud d’Assets distant.
* Pour trouver rapidement un projet en mode Liste où votre système peut contenir de nombreux projets, Adobe prend désormais en charge le tri côté serveur. Les nœuds de projet sont triés sur le serveur principal en fonction de la colonne sélectionnée par l’utilisateur ou l’utilisatrice avant d’effectuer leur rendu dans l’interface utilisateur.
* AEM 6.5.18.0 prend en charge MongoDB, de la version 5.0 à la version 6.0.

### [!DNL Forms]

* **[Amélioration de la gestion des erreurs avec les gestionnaires d’erreurs personnalisés dans l’éditeur de règles](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/standard-validation-error-messages-adaptive-forms.html?lang=fr)** – Vous pouvez désormais appeler une fonction personnalisée (à l’aide de la bibliothèque cliente) en réponse à une erreur renvoyée par un service externe. Vous pouvez également fournir une réponse personnalisée aux utilisateurs finaux et utilisatrices finales. Vous pouvez également effectuer des actions spécifiques pour les erreurs renvoyées par un service. Par exemple, vous pouvez appeler un workflow personnalisé dans le serveur principal pour des codes d’erreur spécifiques ou informer le client ou la cliente que le service ne fonctionne pas.

* **[Amélioration de l’étape de workflow Adobe Sign](https://experienceleague.adobe.com/docs/experience-manager-65/forms/workflows/aem-forms-workflow-step-reference.html?lang=fr#sign-document-step)** – L’étape de workflow Adobe Sign dans les workflows AEM est disponible avec les améliorations suivantes.

   * **Amélioration de la sécurité avec l’authentification par pièce d’identité officielle pour Adobe Sign** – L’authentification par pièce d’identité officielle Adobe Acrobat Sign offre un niveau supplémentaire de vérification. Elle permet aux utilisateurs et utilisatrices d’authentifier leur identité à l’aide d’une pièce d’identité officielle (permis de conduire, carte d’identité nationale, passeport). En utilisant des documents d’identification approuvés, cette amélioration ajoute un niveau de confiance supplémentaire au processus de signature, ce qui en fait une solution idéale pour les scénarios qui nécessitent une sécurité, une conformité et une validation des utilisateurs et utilisatrices renforcées.

   * **Amélioration de la transparence avec le journal d’audit pour les documents Adobe Sign** – Utilisez la fonction Journal d’audit pour obtenir des informations détaillées sur le cycle de vie de vos documents Adobe Sign. Grâce au journal d’audit, vous pouvez désormais conserver un enregistrement complet de toutes les actions et interactions liées à vos documents. Cela inclut des détails tels que les personnes qui ont consulté, modifié ou signé le document, ainsi que l’heure et la date de chaque événement. Cette amélioration est essentielle pour maintenir la conformité, résoudre les litiges et assurer l’intégrité de vos accords numériques.


   * **Extension des rôles des destinataires du contrat au-delà de la seule personne signataire** – Adobe Acrobat Sign vous permet d’étendre les rôles des destinataires du contrat au-delà de la seule personne signataire afin de mieux répondre aux exigences de leur workflow. Lorsque cette option est activée, le rôle de chaque destinataire d’un contrat peut être configuré individuellement, la personne signataire étant la valeur par défaut.


* **[Programme d’installation complet d’AEM Forms on JEE](https://experienceleague.adobe.com/docs/experience-manager-65/forms/install-aem-forms/jee-installation/aem-forms-jee-supported-platforms.html?lang=fr)** – Le pack de services apporte un programme d’installation complet pour AEM Forms on JEE qui prend en charge plusieurs nouvelles combinaisons de logiciels, notamment :
   * Microsoft® Windows Server 2022
   * Microsoft® Active Directory 2022
   * Oracle WebLogic 14C sous Windows Server 2022
   * Red Hat® JBoss® 7.4.10
   * MongoDB 6.0 <!-- it was previously MongoDB 4.4 -->
   * Connecteur 8 JDBC MySQL

Si vous installez ou envisagez d’utiliser les derniers logiciels pour votre environnement AEM Forms 6.5 on JEE, Adobe recommande d’utiliser le programme d’installation complet d’AEM 6.5.18.0 Forms on JEE. Pour consulter la liste complète des logiciels nouvellement ajoutés et obsolètes, reportez-vous à la documentation d’AEM Forms on JEE ou d’AEM Forms on OSGi.

## AEM 6.5, Pack de services 17—25 mai 2023

* **Améliorations de l’expérience de recherche** : vous pouvez désormais effectuer rapidement les opérations suivantes sur les ressources qui s’affichent dans les résultats de recherche :
   * Créer un workflow
   * Créer une version
   * Associer ou dissocier des ressources

  Vous n’avez pas besoin d’accéder à l’emplacement de la ressource et d’afficher ses propriétés pour effectuer ces opérations.
* _Instantané&#x200B;_**Dynamic Media**- Testez des images de test ou des URL Dynamic Media pour voir la sortie de différents modificateurs d’image et les optimisations de l’imagerie dynamique pour la taille de fichier (avec diffusion WebP et AVIF), la bande passante réseau et le rapport pixel de l’appareil. Voir [Instantané Dynamic Media](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/images/dynamic-media-snapshot.html?lang=fr).
* **Streaming DASH avec Dynamic Media** - Prise en charge du nouveau protocole (DASH, Dynamic Adaptive Streaming over HTTP) pour le streaming adaptatif dans les diffusions vidéo Dynamic Media (avec CMAF activé). Disponible maintenant pour toutes les régions, [activé au moyen d’un ticket d’assistance](/help/assets/video.md#enable-dash-on-your-account-enable-dash).
* **Intégration d’Experience Manager Sites et de fragments de contenu à Assets Next-Generation Dynamic Media** - Les utilisateurs et utilisatrices d’Experience Manager Assets as a Cloud Service Next-Generation Dynamic Media peuvent désormais utiliser ces ressources hébergées dans le cloud pour la création et la diffusion avec des instances On-Premise ou Managed Services d’Experience Manager Sites 6.5.

### [!DNL Forms]

* **[Formulaires adaptatifs dans l’éditeur de page AEM](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md)** : vous pouvez désormais utiliser l’éditeur de page AEM pour créer et ajouter rapidement plusieurs formulaires à vos pages Sites. Cette fonctionnalité permet aux auteurs et autrices de contenu de créer des expériences fluides de capture de données dans les pages Sites à l’aide de la puissance des composants de formulaires adaptatifs, notamment le comportement dynamique, les validations, l’intégration de données, la génération d’un document d’enregistrement et l’automatisation de la gestion commerciale. Vous pouvez effectuer les actions suivantes :
   * Créer un formulaire adaptatif en faisant glisser les composants de formulaire vers le composant de conteneur de Forms adaptatif dans l’éditeur AEM Sites ou les fragments d’expérience.
   * Utiliser l’assistant de formulaires adaptatifs dans l’éditeur AEM Sites pour créer des formulaires indépendants de n’importe quelle page Sites, ce qui vous permet de réutiliser ces formulaires sur plusieurs pages.
   * Ajouter plusieurs formulaires à une page Sites, en rationalisant l’expérience client et en offrant une plus grande flexibilité.
* **[Prise en charge de reCAPTCHA Enterprise dans Experience Manager Forms](/help/forms/using/captcha-adaptive-forms.md)** : ajout de la prise en charge de reCAPTCHA Enterprise dans Experience Manager Forms, offrant une meilleure protection contre les activités frauduleuses et les spams, en plus de la prise en charge existante de Google reCAPTCHA v2.
* **[Prise en charge d’Adobe Acrobat Sign pour l’administration avec Experience Manager Forms](/help/forms/using/adobe-sign-integration-adaptive-forms.md)** : AEM Forms s’intègre désormais à Adobe Acrobat Sign pour l’administration (compatible avec FedRAMP). Cette intégration offre un niveau avancé de conformité et de sécurité pour les signatures électroniques avec les envois de formulaires adaptatifs pour les comptes associés au gouvernement (ministères et organismes gouvernementaux). L’intégration à Adobe Acrobat Sign for Government permet aux partenaires d’Adobe et aux clients gouvernementaux d’utiliser des signatures électroniques dans Adaptive Forms pour certains secteurs d’activité les plus critiques et les plus sensibles. Cette couche supplémentaire de sécurité garantit que toutes les signatures électroniques sont entièrement conformes à la norme FedRAMP Moderate, offrant ainsi la tranquillité d’esprit aux clients gouvernementaux d’Adobe.
* **Activation de l’intégration de Salesforce à Experience Manager Forms pour l’échange de données** : configurez l’intégration entre Experience Manager Forms et l’application Salesforce à l’aide du flux d’informations d’identification du client OAuth 2.0. Cette fonctionnalité permet une authentification et une autorisation sécurisées et directes de l’application et offre une communication transparente sans intervention de l’utilisateur ou utilisatrice.
* **Optimisation et fonctionnalité améliorée du moteur de workflow** : augmentez les performances des moteurs de workflow en réduisant le nombre d’instances de workflow. En complément des valeurs de statut `COMPLETED` et `RUNNING`, le workflow prend également en charge trois nouvelles valeurs de statut : `ABORTED`, `SUSPENDED` et `FAILED`.

## AEM 6.5, Pack de services 16—23 février 2023

Prise en charge du nouveau protocole DASH (Dynamic Adaptive Streaming over HTTP) pour la diffusion en continu à débit adaptatif dans les diffusions vidéo Dynamic Media (avec CMAF, le [format d’application de média commun], activé).

* La diffusion en continu à débit adaptatif (DASH/HLS) garantit une meilleure expérience de visionnage des vidéos aux utilisateurs et utilisatrices finaux.
* Largement adopté dans le secteur, DASH est le protocole standard international pour la diffusion en continu à débit adaptatif de vidéos.
* Disponible désormais en Asie-Pacifique et en Amérique du Nord (activable au moyen d’un ticket d’assistance) ; bientôt en Europe, au Moyen-Orient, en Afrique.

Voir [Activer DASH sur votre compte](/help/assets/video.md#enable-dash).

### [!DNL Forms]

* Les [formulaires adaptatifs découplés](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html?lang=fr) permettent aux développeurs et développeuses de créer, publier et gérer des formulaires interactifs accessibles et interactifs via des API, plutôt que par le biais d’une interface utilisateur graphique classique.

* Les [composants principaux des formulaires adaptatifs](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=fr#features) sont un ensemble de 24 composants open source compatibles avec BEM qui sont conçus sur la base des composants principaux de la gestion de contenu web d’Adobe Experience Manager. Ces composants sont en open source et fournissent aux développeurs et développeuses la possibilité de les personnaliser et les étendre facilement pour répondre aux besoins spécifiques de leur entreprise. Toute personne disposant de compétences pour personnaliser les [composants principaux de gestion de contenu web](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/get-started/authoring.html?lang=fr) peut facilement personnaliser et mettre en forme ces composants.

* Le service Reader Extensions sur OSGi fournit désormais des options distinctes permettant d’importer et d’exporter des droits d’utilisation sur un PDF afin d’importer ou d’exporter des données dans Adobe Acrobat Reader.

## AEM 6.5, Pack de services 15—24 novembre 2022

### [!DNL Forms]

* AEM Forms Designer est désormais disponible en [espagnol](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=fr).
* Vous pouvez désormais utiliser [OAuth2 pour l’authentification avec les protocoles de serveur de messagerie Microsoft® Office 365 (SMTP et IMAP)](/help/forms/using/oauth2-support-for-mail-service.md).
* Vous pouvez définir la propriété [Revalider sur le serveur](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions.html?lang=fr#enabling-server-side-validation-br) sur true pour identifier les champs masqués à exclure d’un document d’enregistrement côté serveur.
* AEM Forms Designer nécessite une version 32 bits de Visual C++ 2019 Redistributable (x86).

## AEM 6.5, Pack de services 14—25 août 2022

Correctifs de bogues uniquement.

## AEM 6.5, Pack de services 13—26 mai 2022

* Utilisation du CAPTCHA invisible dans un formulaire adaptatif : vous pouvez désormais utiliser un CAPTCHA invisible pour afficher le défi CAPTCHA uniquement en cas d’activité suspecte. Si aucune activité suspecte n’est détectée, le CAPTCHA ne s’affiche pas. Il permet d’évaluer le remplissage du formulaire par un humain sans exiger de case à cocher, de réduire les efforts de personnalisation et d’améliorer l’expérience de l’utilisateur final.

* Ajout de la prise en charge de la récupération des en-têtes de réponse dans le post-processeur du modèle de données de formulaire pour les points d’entrée REST.

* Désormais, lors de la génération d’un fichier de traduction de formulaire adaptatif, la même séquence de textes que le fichier XLIFF généré est identique à la séquence de composants dans le formulaire adaptatif correspondant.

* Lorsque vous localisez un formulaire adaptatif et apportez même une petite modification au texte de la langue de base, la traduction complète est manquante pour toutes les autres langues. Le problème est corrigé dans [!DNL Experience Manager] 6.5.13.0.

* Améliorations de l’accessibilité pour Forms :

   * Ajout de la prise en charge pour les lecteurs d’écran pour leur permettre de reconnaître l’en-tête et le corps d’un tableau comme des entités continues et connectées. Cela permet aux lecteurs d’écran de naviguer correctement entre les tableaux. (NPR-37139)
   * Ajout de la prise en charge des lecteurs d’écran pour arrêter la navigation dans l’espace de travail de HTML jusqu’à l’ouverture d’une boîte de dialogue. 

## AEM 6.5, Pack de services 12—24 février 2022

* Après la configuration d’une connexion entre les déploiements de gestion des DAM et Sites à distance, les ressources de gestion des DAM à distance sont disponibles pour le déploiement sur Sites. Vous pouvez désormais effectuer les opérations suivantes : mettre à jour, supprimer, renommer et déplacer des opérations sur les ressources ou dossiers de gestion des DAM à distance. Les mises à jour, avec un certain retard, sont disponibles automatiquement sur le déploiement Sites.
* Les déploiements push d’une source de Live Copy vers plusieurs Live Copies sont désormais possibles par défaut, sans nécessiter de configuration de plan directeur.
* Le statut des opérations asynchrones en cours s’affiche désormais dans l’interface utilisateur afin d’empêcher les utilisateurs de déclencher accidentellement plusieurs opérations asynchrones sur le même chemin.
* La prise en charge de l’authentification IMS est fournie pour les API Analytics 2.0.
* Prise en charge de l’API pour le fragment d’expérience de type d’offre JSON.
* La demande d’offre est désormais fournie pour l’option Supprimer l’offre (API de fragment d’expérience) dans IMS.
* Le référentiel intégré (Apache Jackrabbit Oak) reste sur la version 1.22.9.
