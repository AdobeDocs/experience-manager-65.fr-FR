---
title: Les 10 plus grands risques de sécurité OWASP
description: Découvrez comment AEM gère les dix plus grands risques de sécurité OWASP.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
exl-id: 8b2a2f1d-8286-4ba5-8fe2-627509c72a45
feature: Security
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '481'
ht-degree: 100%

---

# Les 10 plus grands risques de sécurité OWASP{#owasp-top}

Le projet [Open Web Application Security Project](https://owasp.org/) (OWASP) conserve une liste de ce qu’il considère comme les [dix plus grands risques de sécurité des applications web](https://owasp.org/www-project-top-ten/).

Ils sont répertoriés ci-dessous, accompagnés d’une explication de la façon dont CRX les traite.

## 1. Injection {#injection}

* SQL -Empêché par défaut : La configuration de référentiel par défaut ne comprend ni ne requiert de base de données traditionnelle et toutes les données sont stockées dans le référentiel de contenu. Tous les accès sont limités aux utilisateurs authentifiés et ne peuvent avoir lieu que via l’API JCR. SQL est pris en charge pour les requêtes de recherche uniquement (SELECT). SQL offre en outre une prise en charge de la liaison des valeurs.
* LDAP : l’injection LDAP n’est pas possible, car le module d’authentification filtre l’entrée et effectue l’importation de l’utilisateur ou de l’utilisatrice à l’aide de la méthode de liaison.
* Système d’exploitation : aucune exécution de shell n’est effectuée dans l’application.

## 2. Cross-Site Scripting (XSS) {#cross-site-scripting-xss}

La solution générale consiste à coder toutes les sorties du contenu créé par l’utilisateur avec une bibliothèque de protection XSS côté serveur basée sur [OWASP Encoder](https://owasp.org/www-project-java-encoder/) et [AntiSamy](https://wiki.owasp.org/index.php/Category:OWASP_AntiSamy_Project).

Le XSS est une priorité majeure pendant le test et le développement et les problèmes détectés sont (généralement) résolus immédiatement.

## 3. Authentification interrompue et gestion des sessions {#broken-authentication-and-session-management}

AEM utilise des techniques d’authentification performantes et éprouvées, qui font appel à [Apache Jackrabbit](https://jackrabbit.apache.org/jcr/index.html) et [Apache Sling](https://sling.apache.org/). Les sessions de navigateur ou HTTP ne sont pas utilisées dans AEM.

## 4. Références d’objets directs non sécurisées {#insecure-direct-object-references}

Tous les accès aux objets de données sont arbitrés par le référentiel et donc restreints par le contrôle d’accès basé sur les rôles.

## 5. Cross-Site Request Forgery (attaque CSRF) {#cross-site-request-forgery-csrf}

Une attaque Cross-Site Request Forgery (CSRF) est arbitrée en injectant automatiquement un jeton cryptographique dans l’ensemble des formulaires et des requêtes AJAX et en vérifiant ce jeton sur le serveur pour chaque requête POST.

En outre, AEM est fourni avec un filtre référent-en-tête, qui peut être configuré pour autoriser *uniquement* les requêtes POST d’hôtes spécifiques (inscrits dans une liste autorisée).

## 6. Erreur de configuration de la sécurité {#security-misconfiguration}

Il est impossible de garantir que tous les logiciels sont toujours correctement configurés. Toutefois, Adobe s’efforce de fournir autant d’assistance que possible et de rendre la configuration aussi simple possible. De plus, AEM comprend des [contrôles d’intégrité de la sécurité intégrés](/help/sites-administering/operations-dashboard.md) qui vous aident à surveiller en un coup d’œil la configuration de la sécurité.

Examinez la [Liste de contrôle de sécurité](/help/sites-administering/security-checklist.md) pour plus d’informations et obtenir des instructions étape par étape.

## 7. Stockage cryptographique non sécurisé {#insecure-cryptographic-storage}

Les mots de passe sont stockés sous la forme de hachages cryptographiques dans le nœud utilisateur. Par défaut, ces nœuds ne sont lisibles que par l’administrateur ou l’administratrice et la personne elle-même.

Les données sensibles telles que les informations d’identification tierces sont stockées sous forme chiffrée à l’aide d’une bibliothèque cryptographique certifiée FIPS 140-2.

## 8. Échec de la limitation de l’accès à l’URL {#failure-to-restrict-url-access}

Le référentiel permet de définir des [autorisations précises (comme spécifié par JCR)](https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/2.0/16_Access_Control_Management.html) pour n’importe quelle personne ou n’importe quel groupe dans n’importe quel chemin d’accès, via des entrées de contrôle d’accès. Les restrictions d’accès sont appliquées par le référentiel.

## 9. Protection insuffisante de la couche de transfert {#insufficient-transport-layer-protection}

Atténuée par la configuration du serveur (par exemple, en utilisant HTTPS uniquement).

## 10. Redirections et transferts non validés {#unvalidated-redirects-and-forwards}

Risque atténué en restreignant toutes les redirections à des destinations fournies par l’utilisateur vers des emplacements internes.
