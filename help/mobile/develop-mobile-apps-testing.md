---
title: Test des applications mobiles
description: Découvrez comment automatiser ou tester manuellement vos applications mobiles à l’aide de divers outils.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing
content-type: reference
exl-id: e10e1904-7016-4eb0-9408-36297285f378
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '954'
ht-degree: 0%

---

# Test des applications mobiles{#testing-mobile-apps}

{{ue-over-mobile}}

Compte tenu de la grande variété d&#39;appareils sur le marché et de la sortie des appareils, il est devenu impératif de tester vos applications. Il s’agit d’un domaine où la fonctionnalité et la convivialité peuvent susciter peu d’avis sur une boutique d’applications, mais un seul défaut peut entraîner la désinstallation de votre application. Vos plans de test et l’assurance qualité doivent faire l’objet d’une attention particulière. Le lien suivant couvre de nombreux sujets qui doivent être abordés en général, comme l’identification de votre environnement, la définition de cas de test, les types de test, les hypothèses et l’implication du client. Vous trouverez également des outils pour faciliter l’effort de test. Des outils internes, tels que [Hobbes](/help/sites-developing/hobbes.md), peuvent vous aider à tester l’interface utilisateur sur le web. [Tough Day](/help/sites-developing/tough-day.md) peut soumettre vos instances à une contrainte lors d’une charge simulée. Si votre environnement de test dispose déjà d’une expérience avec des outils tiers, tels que Selenium, ceux-ci peuvent également être utilisés.

Lors du développement d’une application mobile, de nombreuses nouvelles préoccupations spécifiques aux appareils doivent être prises en compte, ainsi que celles des tests traditionnels.

* Fonctionnel : toutes les exigences sont-elles remplies par votre application ?
* Convivialité - L’application est-elle facile à utiliser et à comprendre pour votre client ?
* Performances : que se passe-t-il lors d’un pic d’utilisation ? Les éléments d’application, tels que les balayages et les carrousels, sont-ils rapides et ne nuisent pas à l’expérience ?
* Échec ou interruptions - Que se passe-t-il lorsqu’un appel ou une notification est entrant pendant l’exécution de votre application ? Que se passe-t-il en cas de panne du réseau ou de mise hors tension ?
* Installation et mises à jour - Comment se passe l’installation ? Comment les mises à jour sont-elles transmises ?
* Technique - Votre application consomme-t-elle trop d&#39;énergie d&#39;un appareil ?
* Localisation - Toutes les zones de votre application sont-elles traduites ?
* Certification - Votre application a-t-elle été certifiée ? Les clients peuvent-ils être certains qu’il respecte toutes les exigences légales en matière de confidentialité des données ?

Vous devez répondre à ces questions lors de vos tests automatisés et manuels.

## Test automatisé {#automated-testing}

Un certain degré d’automatisation des tests doit être effectué pour prendre en compte la variété de tailles d’écran, de contraintes de mémoire, de méthodes d’entrée et de systèmes d’exploitation. Non seulement il couvre de nombreux cas de test, mais il peut également accélérer les tests de régression lors de l’introduction de nouvelles fonctionnalités ou de nouveaux appareils. Idéalement, vos outils d’automatisation doivent réduire ou limiter la duplication des efforts. Utilisez des outils ou des structures afin que votre effort de test soit applicable sur toutes les plateformes. Le graphique suivant présente une structure simplifiée d’un environnement de test pour les tests d’interface utilisateur web et les tests d’applications mobiles. Le côté gauche du graphique présente une série de nœuds Selenium avec des navigateurs. SeleniumGrid peut externaliser des tests d’interface utilisateur web courants vers l’un de ces nœuds. Le hub Selenium peut également se connecter à Appium pour des tests d’applications sur plusieurs plateformes. Seuls les simulateurs sont affichés, mais vous pouvez incorporer des utilitaires adb, pour Android™ et Xcode pour les appareils iOS. Des liens sont fournis plus loin dans ce document pour obtenir des détails spécifiques sur les outils mentionnés.

![chlimage_1](assets/chlimage_1.jpeg)

## Test manuel {#manual-testing}

Outre les tests automatisés, votre application doit passer par un cycle de tests manuels. Les clients qui exécutent l’application sur un appareil réel ne peuvent pas être dupliqués par un script. Là aussi, vous avez beaucoup d&#39;options. Vous pouvez utiliser une plateforme, telle que HockeyApp, pour définir qui a accès et recueillir des commentaires. Vous pouvez également externaliser l’ensemble du processus à un service tel que UTest, ElusiveStars ou Test. Si vous disposez d’un groupe de testeurs internes, mais que les appareils ne varient pas, il existe des services cloud où vous pouvez effectuer des tests manuels sur leur pool d’appareils. L’un des services qui fournit cette fonctionnalité est SauceLabs. Vous pouvez également créer des applications à distance sur PhoneGap Enterprise et les installer sur des appareils locaux comme niveau de test d’acceptation ou de démonstration. Consultez le site web PhoneGap (`https://phonegap.com/`) pour consulter ses dernières fonctionnalités et sa documentation. Quelle que soit l&#39;approche, les tests manuels doivent faire ce qui suit :

* atteindre une grande cible de testeurs,
* tester un grand pool de périphériques (idéalement des périphériques réels, mais des simulateurs/émulateurs si des périphériques réels ne sont pas disponibles),
* fournissez des commentaires informatifs :

   * les rapports d’incident,
   * analyse/suivi,
   * la convivialité,
   * les domaines d&#39;attention,
   * les performances,
   * consommation de données/d’énergie, etc.

## Outils {#tools}

Il existe un large éventail d’outils disponibles pour tester les applications mobiles. Le choix de ceux à utiliser doit être basé sur votre situation spécifique : fonctionnalités, prix, support, couverture, etc. Ce qui suit n’est qu’une brève description de certains des outils et services disponibles.

**Selenium**

* Framework qui inclut une API pour les scripts de test afin d’alimenter WebDriver et de contrôler divers navigateurs.
* Vous pouvez l’utiliser avec Appium pour effectuer des tests sur des appareils réels.
* SeleniumGrid dirige les tests sur les nœuds pour les tests parallèles.
* L’IDE Selenium contribue à réduire l’écriture de cas de test.

Pour plus d’informations, consultez [https://www.selenium.dev/](https://www.selenium.dev/).

**Testdroid**

* Un service de test basé sur le cloud avec des hooks d’intégration continus et des tests d’appareils réels.
* Un moteur de recherche d’applications est inclus pour vérifier la compatibilité des appareils, analyser les journaux, parcourir les vues, prendre des captures d’écran et surveiller les performances.

Pour plus d’informations, voir [https://testdroid.com/](https://testdroid.com/).

**Appium**

* Appium est un framework populaire sur plusieurs plateformes pour automatiser les tests mobiles.
* En outre, un inspecteur est inclus avec des capacités d’enregistrement pour aider les cas de test de code.

Pour plus d’informations, voir [https://appium.io/](https://appium.io/).

**SauceLabs**

* SauceLabs fournit des tests basés sur le cloud et s’intègre avec une intégration continue.
* Les tests s’exécutent automatiquement dans leur environnement cloud ou vous pouvez démarrer un appareil ou une plateforme spécifique et effectuer des tests manuels pour résoudre les problèmes.

Pour plus d’informations, voir [https://saucelabs.com/](https://saucelabs.com/).

<!-- **AppTestNow**

* An outsourcing service that tests your mobile apps.
* Included is a large pool of devices and offers a wide range of types of testing: performance, quality, functional, certification, localization, data consumption, and so on.

For more information, see [https://apptestnow.com/](https://apptestnow.com/). -->

**HockeyApp**

* HockeyApp est soumis à des tests manuels où l&#39;application mobile est envoyée à une boutique d&#39;applications personnelles où les testeurs peuvent la télécharger et l&#39;essayer.

Pour plus d’informations, voir [https://hockeyapp.net/features/](https://hockeyapp.net/features/).

**Jenkins**

* Bien qu’il ne s’agisse pas d’un outil de test, Jenkins est une structure d’intégration continue fournissant la colonne vertébrale pour les tests automatisés. De nombreux plug-ins tiers sont disponibles pour étendre les fonctionnalités. Par exemple, le plug-in SeleniumGrid fournit une interface utilisateur pour aider à gérer le hub et les nœuds Selenium.

Pour plus d’informations, voir [https://www.jenkins.io/](https://www.jenkins.io/) et [https://plugins.jenkins.io/](https://plugins.jenkins.io/).
