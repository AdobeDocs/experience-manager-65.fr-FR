---
title: Test des applications mobiles
seo-title: Test des applications mobiles
description: 'null'
seo-description: 'null'
uuid: 3b402d34-5cab-4280-b8b9-88ad9f8fc5e4
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing
content-type: reference
discoiquuid: 5a98e1bd-f5c1-4f2f-ac02-dbd005dc1de7
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1027'
ht-degree: 2%

---


# Test des applications mobiles{#testing-mobile-apps}

>[!NOTE]
>
>Adobe recommande d’utiliser l’éditeur d’application d’une seule page (SPA) pour les projets nécessitant un rendu côté client basé sur la structure SPA (par exemple, React). [En savoir plus](/help/sites-developing/spa-overview.md).

Compte tenu de la large gamme de périphériques sur le marché et de périphériques en cours de publication, le test de vos applications est devenu extrêmement important. Il s’agit d’une zone dans laquelle les fonctionnalités et la convivialité peuvent faire l’objet de critiques peu élevées sur une boutique d’applications, mais un seul défaut peut entraîner la désinstallation de votre application. Il faut faire attention à vos plans de test et à l&#39;assurance qualité. Le lien suivant couvre de nombreux sujets qui doivent être abordés en général, comme, par exemple, identifier votre environnement, définir les cas de test, les types de test, les hypothèses, la participation du client, etc. Il est également question des outils permettant de participer aux efforts de test. Des outils internes, tels que [Hobbes](/help/sites-developing/hobbes.md), peuvent vous aider à tester l’interface utilisateur en ligne. [Un jour](/help/sites-developing/tough-day.md) difficile peut stresser vos instances avec une charge simulée. Si votre environnement de test a déjà de l&#39;expérience avec des outils tiers, comme le sélénium, ceux-ci peuvent également être utilisés.

Lors du développement d’une application mobile, il existe de nombreuses nouvelles préoccupations spécifiques aux appareils qui doivent être traitées en même temps que celles des tests traditionnels.

* Fonctionnel : toutes les exigences sont-elles satisfaites par votre application ?
* Utilité - L&#39;application est-elle facile à utiliser et à comprendre pour votre client ?
* Performances - Que se passe-t-il lors d&#39;un pic d&#39;utilisation ? Les éléments de l’application, tels que les balayage et les carrousels, sont-ils rapides et ne vous éloignent pas de l’expérience ?
* Echec ou interruptions - Que se passe-t-il lorsqu’un appel ou une notification entrant est en cours d’exécution pour votre application ? Que se passe-t-il en cas de panne de réseau ou de coupure de courant ?
* Installation et mises à jour - Comment se passe l&#39;installation ? Comment les mises à jour sont-elles publiées ?
* Technique - Votre application consomme-t-elle trop de puissance sur un appareil ?
* Localisation - Toutes les zones de votre application sont-elles traduites ?
* Certification - Votre application a-t-elle été certifiée ? Les clients peuvent-ils se fier à ce qu&#39;il respecte toutes les exigences légales en matière de confidentialité des données ?

Vous devez répondre à ces questions lors de vos tests automatisés et manuels.

## Test automatisé {#automated-testing}

Un certain degré de test automatisé devrait être effectué pour couvrir la variété de tailles d&#39;écran, de contraintes de mémoire, de méthodes d&#39;entrée et de systèmes d&#39;exploitation. Non seulement il couvre la plupart des cas de test, mais il peut accélérer les tests de régression lorsque de nouvelles fonctionnalités ou de nouveaux dispositifs sont introduits. Dans l&#39;idéal, vos outils d&#39;automatisation devraient réduire ou limiter la duplication des efforts. Utilisez des outils ou des structures afin que vos efforts de test s’appliquent à toutes les plates-formes. Le graphique suivant présente la structure simplifiée d’un environnement de test pour les tests d’interface utilisateur basés sur le Web et les tests d’applications mobiles. La partie gauche du graphique montre une série de noeuds de sélénium avec des navigateurs. SeleniumGrid peut exécuter des tests d’interface utilisateur Web courants sur n’importe lequel de ces noeuds. Le hub Selenium peut également se connecter à Appium pour des tests d’applications multiplateformes. Seuls les simulateurs sont affichés, mais vous pouvez incorporer des utilitaires adb, for Android et Xcode pour les périphériques iOS. Des liens sont fournis plus loin dans ce document où vous trouverez des détails spécifiques sur les outils mentionnés.

![chlimage_1](assets/chlimage_1.jpeg)

## Test manuel {#manual-testing}

Outre les tests automatisés, votre application doit passer par un cycle de tests manuels. Les clients exécutant l’application sur un périphérique réel ne peuvent pas être dupliqués par un script. Ici aussi, vous avez de nombreuses options. Vous pouvez utiliser une plateforme, telle que HockeyApp, pour définir qui a accès et recueillir des commentaires. Vous pouvez également externaliser l’ensemble du processus vers un service tel que UTest, ElusiveStars ou Testin. Si vous disposez d’un groupe de testeurs internes, mais que les périphériques ne sont pas variés, il existe des services cloud où vous pouvez effectuer des tests manuels sur leur pool de périphériques. SauceLabs est l&#39;un de ces services. Vous pouvez également créer des applications à distance sur PhoneGap Enterprise et les installer sur des périphériques locaux sous forme de tests d’acceptation ou de démonstration. Consultez le site Web [PhoneGap](https://phonegap.com/) pour connaître les dernières fonctionnalités et la documentation la plus récente. Quelle que soit l&#39;approche, les tests manuels doivent être effectués;

* a touché une grande cible de testeurs,
* tester par rapport à un grand nombre de périphériques (idéalement des périphériques réels, mais des simulateurs/émulateurs si des périphériques réels ne sont pas disponibles),
* fournir des commentaires informatifs :

   * rapports de plantage,
   * analytics/tracking,
   * convivialité,
   * les domaines d&#39;attention,
   * performances,
   * consommation de données/d&#39;énergie, etc.

## Outils {#tools}

Un large éventail d&#39;outils est disponible pour tester les applications mobiles. Le choix de ceux à utiliser sera basé sur votre situation spécifique : fonctionnalités, prix, support, couverture, etc. Voici une petite description de certains outils et services disponibles.

**Selenium**

* La structure comprend une API pour les scripts de test pour alimenter WebDriver et contrôler divers navigateurs.
* Vous pouvez l’utiliser conjointement avec Appium pour tester des périphériques réels.
* SeleniumGrid dirige les tests sur les noeuds pour les tests parallèles.
* L&#39;IDE du sélénium aide à réduire l&#39;écriture des cas de test.

For more information see [https://www.seleniumhq.org/](https://www.seleniumhq.org/).

**Testdroid**

* Service de test en mode cloud avec crochets d’intégration continue et tests de périphériques réels.
* Inclut un outil de capture d’écran qui vérifie la compatibilité des périphériques, analyse les journaux, analyse les vues, effectue des captures d’écran et surveille les performances.

Pour plus d’informations, voir [https://testdroid.com/](https://testdroid.com/).

**Appium**

* Appium est un cadre multiplateforme très utilisé pour automatiser les tests mobiles.
* En outre, un inspecteur est inclus avec des capacités d&#39;enregistrement pour aider à coder les cas de test.

Pour plus d’informations, voir [https://appium.io/](https://appium.io/).

**SauceLabs**

* SauceLabs fournit des tests basés sur le cloud et s’intègre en continu.
* Les tests s’exécutent automatiquement dans leur environnement cloud ou vous pouvez début un périphérique ou une plateforme spécifique et effectuer des tests manuels pour aider à déboguer les problèmes.

Pour plus d’informations, voir [https://saucelabs.com/](https://saucelabs.com/).

**AppTestNow**

* Service d’externalisation qui teste vos applications mobiles.
* Comprend un grand nombre de périphériques et d&#39;offres, ainsi qu&#39;un large éventail de types de tests : performances, qualité, fonctionnalité, certification, localisation, consommation de données, etc.

Pour plus d’informations, voir [https://www.apptestnow.com](https://www.apptestnow.com/).

**HockeyApp**

* HockeyApp tombe sous le test manuel où l&#39;application mobile est envoyée dans une boutique d&#39;applications personnelle où les testeurs peuvent télécharger et essayer.

Pour plus d’informations, voir [https://hockeyapp.net/features/](https://hockeyapp.net/features/).

**Jenkins**

* Bien qu&#39;il ne s&#39;agisse pas d&#39;un outil de test, Jenkins est un cadre d&#39;intégration continue qui constitue la colonne vertébrale des tests automatisés. De nombreux modules externes tiers sont disponibles pour étendre les fonctionnalités. Par exemple, le module externe SeleniumGrid fournit une interface utilisateur pour aider à gérer le hub et les noeuds du sélénium.

Pour plus d’informations, voir [https://jenkins-ci.org/](https://jenkins-ci.org/) et [https://wiki.jenkins-ci.org/display/JENKINS/Plugins](https://wiki.jenkins-ci.org/display/JENKINS/Plugins).
