---
title: Les 10 plus grands risques d’OWASP
seo-title: OWASP Top 10
description: Découvrez comment AEM gère les 10 plus grands risques de sécurité OWASP.
seo-description: Learn how AEM deals with the top 10 OWASP security risks.
uuid: a5a7e130-e15b-47ae-ba21-448f9ac76074
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: e5323ae8-bc37-4bc6-bca6-9763e18c8e76
exl-id: 8b2a2f1d-8286-4ba5-8fe2-627509c72a45
feature: Security
source-git-commit: 2bae11eafb875f01602c39c0dba00a888e11391a
workflow-type: ht
source-wordcount: '496'
ht-degree: 100%

---

# Les 10 plus grands risques d’OWASP{#owasp-top}

Le projet [Open Web Application Security Project](https://www.owasp.org) (OWASP) tient à jour une liste de ce qu’il considère comme les [10 plus grands risques de sécurité liés aux applications web](https://www.owasp.org/index.php/OWASP_Top_Ten_Project).

Ces risques sont répertoriés ci-dessous, avec une explication sur la manière dont ils sont gérés par CRX.

## 1. Injection {#injection}

* SQL -Empêché par défaut : La configuration de référentiel par défaut ne comprend ni ne requiert de base de données traditionnelle et toutes les données sont stockées dans le référentiel de contenu. Tous les accès sont limités aux utilisateurs authentifiés et ne peuvent avoir lieu que via l’API JCR. SQL est pris en charge pour les requêtes de recherche uniquement (SELECT). SQL offre en outre une prise en charge de la liaison des valeurs.
* LDAP : L’injection LDAP est impossible, car le module d’authentification filtre l’entrée et exécute l’importation des utilisateurs à l’aide de la méthode de liaison.
* OS : Aucune exécution shell n’est effectuée dans l’application.

## 2. Cross-Site Scripting (XSS) {#cross-site-scripting-xss}

La solution générale consiste à coder toutes les sorties du contenu créé par l’utilisateur avec une bibliothèque de protection XSS côté serveur basée sur [OWASP Encoder](https://www.owasp.org/index.php/OWASP_Java_Encoder_Project) et [AntiSamy](https://www.owasp.org/index.php/Category:OWASP_AntiSamy_Project).

Le XSS est une priorité majeure pendant le test et le développement et les problèmes détectés sont (généralement) résolus immédiatement.

## 3. Authentification interrompue et gestion des sessions {#broken-authentication-and-session-management}

AEM utilise des techniques d’authentification performantes et éprouvées, qui font appel à [Apache Jackrabbit](https://jackrabbit.apache.org/) et [Apache Sling](https://sling.apache.org/). Les sessions de navigateur ou HTTP ne sont pas utilisées dans AEM.

## 4. Références d’objets directes non sécurisées {#insecure-direct-object-references}

Tous les accès aux objets de données sont arbitrés par le référentiel et donc restreints par le contrôle d’accès basé sur les rôles.

## 5. Cross-Site Request Forgery (CSRF) {#cross-site-request-forgery-csrf}

Une attaque Cross-Site Request Forgery (CSRF) est arbitrée en injectant automatiquement un jeton cryptographique dans l’ensemble des formulaires et des requêtes AJAX et en vérifiant ce jeton sur le serveur pour chaque requête POST.

En outre, AEM est fourni avec un filtre référent-en-tête, qui peut être configuré pour autoriser *uniquement* les requêtes POST d’hôtes spécifiques (inscrits dans une liste autorisée).

## 6. Configuration incorrecte de la sécurité {#security-misconfiguration}

Il est impossible de garantir que tous les logiciels sont toujours correctement configurés. Toutefois, nous nous efforçons de fournir autant d’assistance que possible et de rendre la configuration aussi simple possible. En outre, AEM est fourni avec des [contrôles d’intégrité intégrés de la sécurité](/help/sites-administering/operations-dashboard.md) qui vous aident à surveiller la configuration de la sécurité en un clin d’œil.

Veuillez examiner la [Liste de contrôle de sécurité](/help/sites-administering/security-checklist.md) pour plus d’informations et obtenir des instructions étape par étape.

## 7. Stockage cryptographique non sécurisé {#insecure-cryptographic-storage}

Les mots de passe sont stockés en tant que hachages cryptographiques dans le nœud d’utilisateur ; par défaut, ces nœuds sont lisibles uniquement par l’administrateur et par l’utilisateur lui-même.

Les données sensibles telles que les identifiants tiers sont stockées dans un formulaire chiffré à l’aide d’une bibliothèque cryptographique certifiée FIPS 140-2.

## 8. Échec de la restriction de l’accès à l’URL {#failure-to-restrict-url-access}

Le référentiel permet de définir des [autorisations précises (comme spécifié par JCR)](https://www.adobe.io/experience-manager/reference-materials/spec/jcr/2.0/16_Access_Control_Management.html) pour n’importe quel utilisateur ou groupe dans n’importe quel chemin d’accès, via des entrées de contrôle d’accès. Les restrictions d’accès sont appliquées par le référentiel.

## 9. Protection insuffisante de la couche de transfert {#insufficient-transport-layer-protection}

Atténué par la configuration du serveur (par exemple, utilisez HTTPS uniquement).

## 10. Redirections et transferts non validés {#unvalidated-redirects-and-forwards}

Risque atténué en restreignant toutes les redirections à des destinations fournies par l’utilisateur vers des emplacements internes.
