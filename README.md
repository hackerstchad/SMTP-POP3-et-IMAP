# 📧 GUIDE AVANCÉ DES PROTOCOLES DE MESSAGERIE ÉLECTRONIQUE

## SMTP · POP3 · IMAP

---

**Auteur :** `hackers_tchad`  
**Date de publication :** 2026  
**Version :** 3.0 - Édition Avancée  
**Licence :** Documentation technique libre  
**Langue :** Français  
**Niveau :** Débutant à Expert  


# TABLE DES MATIÈRES

1. [Introduction générale](#introduction-générale)
2. [Historique et créateurs](#historique-et-créateurs)
3. [Architecture globale de la messagerie](#architecture-globale-de-la-messagerie)
4. [SMTP - Simple Mail Transfer Protocol](#smtp---simple-mail-transfer-protocol)
5. [POP3 - Post Office Protocol version 3](#pop3---post-office-protocol-version-3)
6. [IMAP - Internet Message Access Protocol](#imap---internet-message-access-protocol)
7. [Comparaison SMTP vs POP3 vs IMAP](#comparaison-smtp-vs-pop3-vs-imap)
8. [Sécurité des protocoles email](#sécurité-des-protocoles-email)
9. [Configuration des serveurs et clients](#configuration-des-serveurs-et-clients)
10. [Commandes de vérification sur Linux](#commandes-de-vérification-sur-linux)
11. [Commandes de vérification sur Windows](#commandes-de-vérification-sur-windows)
12. [Opérations pratiques et envoi de messages](#opérations-pratiques-et-envoi-de-messages)
13. [Applications et logiciels utilisés](#applications-et-logiciels-utilisés)
14. [Ressources, livres et liens](#ressources-livres-et-liens)
15. [Annexes techniques](#annexes-techniques)
16. [Glossaire](#glossaire)
17. [FAQ](#faq)
18. [Dépannage et troubleshooting](#dépannage-et-troubleshooting)
19. [Bonnes pratiques](#bonnes-pratiques)
20. [Conclusion](#conclusion)

---

# INTRODUCTION GÉNÉRALE

La messagerie électronique, communément appelée email, est l'un des services les plus anciens et les plus utilisés d'Internet. Elle permet l'échange de messages textuels, de fichiers attachés, de documents et de médias entre utilisateurs du monde entier. Au cœur de ce système se trouvent trois protocoles fondamentaux qui assurent respectivement l'envoi, la réception et la gestion des messages : **SMTP**, **POP3** et **IMAP**.

Ces protocoles ont été développés dans les années 1980 et 1990, à une époque où Internet commençait à se démocratiser au sein des universités, des centres de recherche et des entreprises. Leur conception, bien qu'ancienne, a évolué pour intégrer les exigences modernes en matière de sécurité, de performance et de mobilité.

## Pourquoi ce guide ?

Ce guide a pour objectif de fournir une ressource complète, technique et pratique pour comprendre, configurer, administrer et dépanner les protocoles de messagerie. Que vous soyez étudiant, administrateur système, développeur, consultant en sécurité ou simple utilisateur curieux, ce document vous accompagnera pas à pas dans l'univers des emails.

## Public cible

- Administrateurs système et réseau
- Ingénieurs DevOps et SRE
- Développeurs d'applications de messagerie
- Consultants en cybersécurité
- Étudiants en informatique et réseaux
- Passionnés de technologie et de protocoles Internet

## Contenu de ce guide

Ce document couvre en profondeur :

- Les principes fondamentaux de SMTP, POP3 et IMAP
- L'historique et les créateurs de ces protocoles
- L'architecture client-serveur de la messagerie
- Les ports, les codes de réponse et les commandes
- Les mécanismes d'authentification et de chiffrement
- Les configurations des serveurs (Postfix, Sendmail, Dovecot, Exchange, etc.)
- Les configurations des clients (Outlook, Thunderbird, Apple Mail, etc.)
- Les commandes de vérification sous Linux et Windows
- Les opérations pratiques : envoi, réception, diagnostic
- Les outils, applications et ressources complémentaires
- Les bonnes pratiques de sécurité et de performance

---

# HISTORIQUE ET CRÉATEURS

## Origines de la messagerie électronique

Avant l'existence d'Internet tel que nous le connaissons, des systèmes de messagerie électronique existaient déjà au sein des grands ordinateurs centraux. Le premier système de messagerie électronique est généralement attribué à **Ray Tomlinson** en 1971, qui a envoyé le premier message entre deux machines sur le réseau ARPANET. Il a choisi le symbole `@` pour séparer le nom de l'utilisateur du nom de la machine hôte.

## Ray Tomlinson (1941-2016)

Raymond Samuel Tomlinson était un programmeur américain qui a implémenté le premier système de courrier électronique sur ARPANET. Son travail a posé les bases de l'adressage email moderne avec la syntaxe `utilisateur@domaine`.

## Évolution des standards

Avec la croissance d'ARPANET puis d'Internet, il est devenu nécessaire de standardiser le format des messages et les protocoles d'échange. C'est ainsi que sont nés SMTP, POP et IMAP, chacun répondant à des besoins spécifiques.

## SMTP - Simple Mail Transfer Protocol

- **Créateur principal :** Jonathan Bruce Postel
- **Première RFC :** RFC 821 (août 1982)
- **RFC actuelle :** RFC 5321 (octobre 2008)
- **Objectif :** Transférer des messages électroniques d'un serveur à un autre

### Jonathan Bruce Postel

Jonathan Postel (1943-1998) était un informaticien américain, pionnier d'Internet. Il a dirigé l'IANA (Internet Assigned Numbers Authority) et a contribué à de nombreuses RFC. Il est souvent considéré comme l'un des "pères fondateurs" d'Internet.

## POP - Post Office Protocol

- **Créateur :** Mark Crispin (Université de Stanford)
- **Première version :** POP1 (RFC 918, octobre 1984)
- **POP2 :** RFC 937 (février 1985)
- **POP3 :** RFC 1081 (novembre 1988), puis RFC 1939 (mai 1996)
- **RFC actuelle :** RFC 1939 avec extensions
- **Objectif :** Permettre à un client de récupérer ses emails depuis un serveur

### Mark Crispin

Mark Crispin est un informaticien américain connu pour avoir développé le protocole IMAP et contribué à POP. Il a travaillé à l'Université de Washington et a joué un rôle clé dans l'évolution de la messagerie.

## IMAP - Internet Message Access Protocol

- **Créateur :** Mark Crispin
- **Première version :** IMAP2 (RFC 1064, juillet 1988)
- **RFC actuelle :** RFC 3501 (mars 2003), RFC 9051 (IMAP4rev2, mars 2021)
- **Objectif :** Accéder et gérer des messages électroniques directement sur le serveur

## Frise chronologique

| Année | Événement |
|-------|-----------|
| 1971 | Premier email envoyé par Ray Tomlinson |
| 1973 | Développement des premiers systèmes de messagerie sur ARPANET |
| 1980 | Publication de la RFC 772 (proposition SMTP) |
| 1982 | RFC 821 : SMTP devient un standard officiel |
| 1984 | RFC 918 : Première version de POP |
| 1985 | RFC 937 : POP2 |
| 1988 | RFC 1081 : POP3 ; RFC 1064 : IMAP2 |
| 1996 | RFC 1939 : POP3 standardisé |
| 2003 | RFC 3501 : IMAP4rev1 standardisé |
| 2008 | RFC 5321 : SMTP mis à jour |
| 2012 | RFC 6797 : HSTS pour la sécurité web |
| 2018 | RFC 8461 : SMTP MTA-STS pour sécuriser SMTP |
| 2021 | RFC 9051 : IMAP4rev2 |

---

# ARCHITECTURE GLOBALE DE LA MESSAGERIE

## Modèle client-serveur

La messagerie électronique repose sur un modèle client-serveur. Trois types d'entités principales interagissent :

1. **MUA (Mail User Agent) :** Le client email utilisé par l'utilisateur (Outlook, Thunderbird, etc.)
2. **MTA (Mail Transfer Agent) :** Le serveur qui route et transfère les emails (Postfix, Sendmail, Exchange)
3. **MDA (Mail Delivery Agent) :** Le serveur qui dépose les emails dans la boîte aux lettres de l'utilisateur (Dovecot, Cyrus, Procmail)

## Flux d'un email

```
[Expéditeur MUA] --SMTP--> [MTA expéditeur] --SMTP--> [MTA destinataire] --LDA/MDA--> [Boîte aux lettres] <--POP3/IMAP-- [Destinataire MUA]
```

### Étapes détaillées

1. L'utilisateur rédige un message dans son MUA (client email).
2. Le MUA envoie le message au MTA sortant via SMTP, généralement avec authentification.
3. Le MTA sortant effectue une résolution DNS pour trouver le serveur de messagerie du domaine destinataire.
4. Le MTA destinataire reçoit le message via SMTP sur le port 25.
5. Le message est transmis à un MDA qui le stocke dans la boîte aux lettres de l'utilisateur.
6. Le destinataire utilise son MUA pour récupérer le message via POP3 ou IMAP.

## Composants d'un système de messagerie

### MUA (Mail User Agent)

Le MUA est l'interface utilisateur permettant de lire, rédiger et organiser les emails. Exemples :

- Mozilla Thunderbird
- Microsoft Outlook
- Apple Mail
- Evolution
- Roundcube (webmail)
- Gmail (interface web)

### MTA (Mail Transfer Agent)

Le MTA est responsable du routage et du transfert des emails entre serveurs. Exemples :

- Postfix
- Sendmail
- Exim
- Microsoft Exchange
- Qmail

### MDA (Mail Delivery Agent)

Le MDA reçoit les emails du MTA et les place dans la boîte aux lettres de l'utilisateur. Exemples :

- Dovecot LDA
- Procmail
- Maildrop
- Cyrus IMAP

### MX Record (Mail Exchanger)

Un enregistrement DNS de type MX indique quel serveur est responsable de la réception des emails pour un domaine donné. Exemple :

```dns
example.com.    IN    MX    10    mail.example.com.
example.com.    IN    MX    20    backup-mail.example.com.
```

## Ports standard et sécurisés

| Protocole | Port standard | Port sécurisé (TLS/SSL) | Port de soumission |
|-----------|---------------|-------------------------|--------------------|
| SMTP      | 25            | 465 (SMTPS)             | 587 (Submission)   |
| POP3      | 110           | 995 (POP3S)             | -                  |
| IMAP      | 143           | 993 (IMAPS)             | -                  |

---

# SMTP - SIMPLE MAIL TRANSFER PROTOCOL

## Définition

SMTP (Simple Mail Transfer Protocol) est le protocole standard utilisé pour envoyer des emails sur Internet. Il est responsable du transport des messages depuis le client de l'expéditeur jusqu'au serveur du destinataire, en passant par d'éventuels serveurs intermédiaires.

## Caractéristiques principales

- Protocole de couche application du modèle TCP/IP
- Utilise TCP comme protocole de transport
- Port par défaut : 25 (relai entre serveurs), 587 (soumission client-serveur), 465 (SMTPS)
- Mode texte avec commandes et réponses lisibles
- Basé sur un modèle store-and-forward (stocker et retransmettre)
- Supporte l'authentification (SMTP AUTH)
- Supporte le chiffrement via TLS (STARTTLS)

## Fonctionnement de SMTP

SMTP fonctionne selon un dialogue entre client et serveur. Le client envoie des commandes, et le serveur répond avec des codes numériques accompagnés d'un message textuel.

### Exemple de session SMTP simple

```smtp
220 mail.example.com ESMTP Postfix
HELO client.example.com
250 mail.example.com
MAIL FROM:<alice@example.com>
250 2.1.0 Ok
RCPT TO:<bob@destination.com>
250 2.1.5 Ok
DATA
354 End data with <CR><LF>.<CR><LF>
Subject: Test
From: alice@example.com
To: bob@destination.com

Bonjour Bob,
Ceci est un test.
.
250 2.0.0 Ok: queued as ABC123
QUIT
221 2.0.0 Bye
```

## Commandes SMTP essentielles

| Commande | Description |
|----------|-------------|
| `HELO`   | Identification du client (ancienne commande) |
| `EHLO`   | Identification du client avec support des extensions |
| `MAIL FROM:` | Spécifie l'expéditeur du message |
| `RCPT TO:`   | Spécifie le destinataire du message |
| `DATA`   | Indique le début du contenu du message |
| `RSET`   | Réinitialise la transaction en cours |
| `VRFY`   | Vérifie l'existence d'un utilisateur |
| `EXPN`   | Liste les membres d'une liste de diffusion |
| `HELP`   | Affiche l'aide sur les commandes disponibles |
| `QUIT`   | Termine la session |
| `AUTH`   | Authentifie le client |
| `STARTTLS` | Démarre une session TLS |

## Codes de réponse SMTP

Les codes de réponse SMTP sont des nombres à trois chiffres. Le premier chiffre indique la catégorie de la réponse.

### Catégories de codes

| Code | Signification |
|------|---------------|
| 2xx  | Succès |
| 3xx  | Information complémentaire requise |
| 4xx  | Erreur temporaire (retry possible) |
| 5xx  | Erreur permanente |

### Codes courants

| Code | Signification |
|------|---------------|
| 220  | Service prêt |
| 221  | Fermeture du canal de transmission |
| 235  | Authentification réussie |
| 250  | Action demandée effectuée |
| 251  | Utilisateur non local, message transmis |
| 354  | Début du contenu du message |
| 421  | Service non disponible |
| 450  | Boîte aux lettres indisponible |
| 451  | Erreur locale de traitement |
| 452  | Espace insuffisant |
| 500  | Erreur de syntaxe |
| 501  | Paramètre incorrect |
| 502  | Commande non implémentée |
| 503  | Mauvaise séquence de commandes |
| 504  | Paramètre non implémenté |
| 550  | Boîte aux lettres introuvable |
| 551  | Utilisateur non local |
| 552  | Message trop grand |
| 553  | Nom de boîte aux lettres incorrect |
| 554  | Transaction échouée |

## Extensions SMTP (ESMTP)

ESMTP (Extended SMTP) ajoute des fonctionnalités au protocole de base. Lorsqu'un client utilise `EHLO`, le serveur répond avec la liste des extensions supportées.

### Extensions courantes

- **STARTTLS :** Chiffrement TLS
- **AUTH :** Authentification (PLAIN, LOGIN, CRAM-MD5, etc.)
- **SIZE :** Taille maximale acceptée pour un message
- **PIPELINING :** Envoi de plusieurs commandes sans attendre chaque réponse
- **DSN :** Notification d'état de livraison
- **ENHANCEDSTATUSCODES :** Codes d'état améliorés
- **8BITMIME :** Support des caractères 8 bits
- **SMTPUTF8 :** Support des caractères UTF-8 dans les adresses

## Format d'un message SMTP

Un message email se compose de deux parties : l'en-tête et le corps.

### Exemple de message

```email
Return-Path: <alice@example.com>
Received: from client.example.com (client.example.com [192.168.1.10])
    by mail.example.com (Postfix) with ESMTP id ABC123
    for <bob@destination.com>; Mon, 15 Jan 2026 10:30:00 +0100 (CET)
Message-ID: <unique-id@example.com>
Date: Mon, 15 Jan 2026 10:30:00 +0100
From: Alice <alice@example.com>
To: Bob <bob@destination.com>
Subject: Exemple de message
MIME-Version: 1.0
Content-Type: text/plain; charset=UTF-8
Content-Transfer-Encoding: 7bit

Bonjour Bob,

Voici le corps du message.

Cordialement,
Alice
```

## SMTP et DNS

Lors de l'envoi d'un email, le serveur expéditeur doit déterminer quel serveur est responsable de la réception des emails pour le domaine du destinataire. Il utilise pour cela les enregistrements MX.

### Exemple de requête MX

```bash
# Linux
$ dig MX example.com +short
10 mail.example.com.
20 backup.example.com.

# Windows PowerShell
Resolve-DnsName -Name example.com -Type MX
```

## SMTP AUTH

L'authentification SMTP empêche l'utilisation non autorisée du serveur pour envoyer du spam. Les mécanismes courants incluent :

- **PLAIN :** Envoi du nom d'utilisateur et du mot de passe en clair (nécessite TLS)
- **LOGIN :** Similaire à PLAIN mais avec un encodage base64
- **CRAM-MD5 :** Utilise un défi-réponse pour éviter d'envoyer le mot de passe en clair
- **XOAUTH2 :** Utilisé par Gmail et les services modernes

## STARTTLS et SMTPS

- **STARTTLS :** Négociation TLS après connexion initiale en clair (port 25 ou 587)
- **SMTPS :** SMTP sur SSL/TLS dès la connexion (port 465)

L'utilisation de TLS est fortement recommandée pour protéger les identifiants et le contenu des messages.

## Où utilise-t-on SMTP ?

SMTP est utilisé partout où des emails sont envoyés :

- Clients de messagerie (Outlook, Thunderbird)
- Webmails (Gmail, Outlook.com, Yahoo Mail)
- Applications web (formulaires de contact, notifications)
- Scripts et automatisations (backups, alertes système)
- Serveurs de messagerie d'entreprise
- Plateformes de marketing par email
- Systèmes IoT et objets connectés

---

# POP3 - POST OFFICE PROTOCOL VERSION 3

## Définition

POP3 (Post Office Protocol version 3) est un protocole utilisé par un client de messagerie pour récupérer des emails depuis un serveur distant. Par défaut, POP3 télécharge les messages sur l'appareil local et les supprime généralement du serveur.

## Caractéristiques principales

- Protocole de réception d'emails
- Port standard : 110
- Port sécurisé : 995 (POP3S)
- Fonctionnement simple et léger
- Téléchargement des messages sur le client
- Mode déconnecté après récupération
- Peu gourmand en bande passante une fois les messages téléchargés

## Fonctionnement de POP3

POP3 établit une connexion entre le client et le serveur, puis permet au client de lister, de récupérer et de supprimer des messages.

### États d'une session POP3

1. **AUTHORIZATION :** Authentification de l'utilisateur
2. **TRANSACTION :** Consultation et gestion des messages
3. **UPDATE :** Application des suppressions et fermeture

### Exemple de session POP3

```pop3
+OK POP3 server ready
USER alice
+OK
PASS secretpassword
+OK alice has 3 messages
STAT
+OK 3 1500
LIST
+OK 3 messages
1 500
2 700
3 300
.
RETR 1
+OK 500 octets
[contenu du message]
.
DELE 1
+OK message 1 deleted
QUIT
+OK POP3 server signing off
```

## Commandes POP3 essentielles

| Commande | Description |
|----------|-------------|
| `USER`   | Nom d'utilisateur |
| `PASS`   | Mot de passe |
| `STAT`   | Nombre et taille totale des messages |
| `LIST`   | Liste des messages avec leur taille |
| `RETR`   | Récupère un message |
| `DELE`   | Marque un message pour suppression |
| `NOOP`   | Ne fait rien (garde la session active) |
| `RSET`   | Réinitialise les marques de suppression |
| `QUIT`   | Termine la session et applique les suppressions |
| `TOP`    | Récupère les premières lignes d'un message |
| `UIDL`   | Liste les identifiants uniques des messages |
| `APOP`   | Authentification sécurisée par défi-réponse |

## Réponses POP3

Les réponses POP3 commencent par `+OK` en cas de succès ou `-ERR` en cas d'erreur.

| Réponse | Signification |
|---------|---------------|
| `+OK`   | Commande réussie |
| `-ERR`  | Erreur |

## Modes de fonctionnement de POP3

### Mode par défaut

Par défaut, POP3 télécharge les messages sur le client et les supprime du serveur. Cela libère de l'espace sur le serveur mais ne permet pas d'accéder aux messages depuis plusieurs appareils.

### Mode conservation sur le serveur

La plupart des clients POP3 offrent une option pour conserver une copie des messages sur le serveur pendant un certain temps. Cela permet un accès multi-appareils partiel.

### Avantages de POP3

- Simple à configurer
- Faible consommation de ressources serveur
- Idéal pour les connexions lentes ou instables
- Messages disponibles hors ligne une fois téléchargés
- Libère l'espace serveur

### Inconvénients de POP3

- Pas de synchronisation multi-appareils native
- Pas de gestion avancée des dossiers sur le serveur
- Suppression par défaut des messages sur le serveur
- Moins adapté aux usages mobiles modernes

## Où utilise-t-on POP3 ?

POP3 est utilisé dans des contextes spécifiques :

- Utilisateurs avec une seule machine de messagerie
- Environnements avec une connectivité limitée
- Sauvegarde locale des emails
- Systèmes embarqués ou anciens clients
- Fournisseurs d'accès Internet historiques

---

# IMAP - INTERNET MESSAGE ACCESS PROTOCOL

## Définition

IMAP (Internet Message Access Protocol) est un protocole permettant à un client de messagerie d'accéder à des emails stockés sur un serveur distant. Contrairement à POP3, IMAP garde les messages sur le serveur et synchronise l'état (lus, non lus, dossiers, drapeaux) entre plusieurs appareils.

## Caractéristiques principales

- Protocole de gestion avancée des emails sur serveur
- Port standard : 143
- Port sécurisé : 993 (IMAPS)
- Synchronisation multi-appareils
- Gestion des dossiers sur le serveur
- Support des drapeaux (lus, répondu, important, etc.)
- Recherche côté serveur
- Téléchargement sélectif des messages

## Fonctionnement de IMAP

IMAP maintient les messages sur le serveur et permet au client d'effectuer des opérations comme lister les dossiers, rechercher des messages, récupérer des en-têtes ou le contenu complet, et définir des drapeaux.

### Exemple de session IMAP

```imap
* OK [CAPABILITY IMAP4rev1 SASL-IR LOGIN-REFERRALS ID ENABLE IDLE LITERAL+ AUTH=PLAIN AUTH=LOGIN] Dovecot ready.
a1 LOGIN alice secretpassword
a1 OK [CAPABILITY IMAP4rev1 SASL-IR LOGIN-REFERRALS ID ENABLE IDLE SORT SORT=DISPLAY THREAD=REFERENCES THREAD=REFS THREAD=ORDEREDSUBJECT MULTIAPPEND URL-PARTIAL CATENATE UNSELECT CHILDREN NAMESPACE UIDPLUS LIST-EXTENDED I18NLEVEL=1 CONDSTORE QRESYNC ESEARCH ESORT SEARCHRES WITHIN CONTEXT=SEARCH LIST-STATUS BINARY MOVE SNIPPET=FUZZY PREVIEW=FUZZY STATUS=SIZE SAVEDATE LITERAL+ NOTIFY SPECIAL-USE] Logged in
a2 LIST "" "*"
* LIST (\HasNoChildren) "/" INBOX
* LIST (\HasNoChildren \Trash) "/" Trash
* LIST (\HasNoChildren \Sent) "/" Sent
a2 OK List completed.
a3 SELECT INBOX
* FLAGS (\Answered \Flagged \Deleted \Seen \Draft)
* OK [PERMANENTFLAGS (\Answered \Flagged \Deleted \Seen \Draft \*)] Flags permitted.
* 3 EXISTS
* 0 RECENT
* OK [UIDVALIDITY 1234567890] UIDs valid
* OK [UIDNEXT 4] Predicted next UID
a3 OK [READ-WRITE] Select completed.
a4 FETCH 1:3 (FLAGS BODY[HEADER.FIELDS (SUBJECT FROM DATE)])
* 1 FETCH (FLAGS (\Seen) SUBJECT "Bienvenue" FROM "admin@example.com" DATE "Mon, 15 Jan 2026 09:00:00 +0100")
* 2 FETCH (FLAGS () SUBJECT "Réunion" FROM "boss@example.com" DATE "Mon, 15 Jan 2026 10:00:00 +0100")
* 3 FETCH (FLAGS (\Answered) SUBJECT "Retour" FROM "client@example.com" DATE "Mon, 15 Jan 2026 11:00:00 +0100")
a4 OK Fetch completed.
a5 LOGOUT
* BYE Logging out
a5 OK Logout completed.
```

## Commandes IMAP essentielles

| Commande | Description |
|----------|-------------|
| `LOGIN`  | Authentification |
| `LOGOUT` | Fermeture de session |
| `SELECT` | Sélectionne une boîte aux lettres en mode lecture-écriture |
| `EXAMINE`| Sélectionne une boîte en mode lecture seule |
| `LIST`   | Liste les boîtes aux lettres |
| `LSUB`   | Liste les boîtes aux lettres abonnées |
| `STATUS` | Retourne les informations d'une boîte |
| `CREATE` | Crée une boîte aux lettres |
| `DELETE` | Supprime une boîte aux lettres |
| `RENAME` | Renomme une boîte aux lettres |
| `SUBSCRIBE` | Abonnement à une boîte |
| `UNSUBSCRIBE` | Désabonnement |
| `APPEND` | Ajoute un message à une boîte |
| `FETCH`  | Récupère des données sur des messages |
| `STORE`  | Modifie les drapeaux des messages |
| `COPY`   | Copie des messages vers une autre boîte |
| `UID`    | Préfixe pour utiliser les UIDs |
| `SEARCH` | Recherche de messages |
| `EXPUNGE`| Supprime définitivement les messages marqués |
| `CLOSE`  | Ferme la boîte sélectionnée |
| `NOOP`   | Garde la session active |
| `CAPABILITY` | Liste les capacités du serveur |
| `STARTTLS` | Démarre TLS |
| `IDLE`   | Attend les nouveaux messages en temps réel |

## Réponses IMAP

Les commandes IMAP sont précédées d'un tag choisi par le client. Le serveur répond avec des données non sollicitées (préfixées par `*`) et des réponses finales (avec le tag).

| Préfixe | Signification |
|---------|---------------|
| `* `    | Réponse non sollicitée (données) |
| `+ `    | Continuation requise |
| `tag OK`| Commande réussie |
| `tag NO`| Commande échouée |
| `tag BAD`| Erreur de syntaxe |

## Drapeaux IMAP

Les drapeaux permettent de marquer l'état d'un message.

| Drapeau | Signification |
|---------|---------------|
| `\Seen`      | Message lu |
| `\Answered`  | Répondu |
| `\Flagged`   | Important |
| `\Deleted`   | Marqué pour suppression |
| `\Draft`     | Brouillon |
| `\Recent`    | Message récent |

## Avantages de IMAP

- Accès aux emails depuis plusieurs appareils
- Synchronisation complète (messages, dossiers, drapeaux)
- Gestion centralisée sur le serveur
- Recherche rapide côté serveur
- Pas de risque de perte en cas de panne locale
- Support des dossiers partagés

## Inconvénients de IMAP

- Nécessite une connexion constante pour un fonctionnement optimal
- Plus gourmand en ressources serveur
- Consommation de bande passante plus élevée
- Configuration légèrement plus complexe

## Où utilise-t-on IMAP ?

IMAP est le protocole dominant aujourd'hui :

- Services de messagerie modernes (Gmail, Outlook.com, Yahoo)
- Entreprises avec accès multi-appareils
- Webmails et applications mobiles
- Collaboration et dossiers partagés
- Archivage centralisé

---

# COMPARAISON SMTP VS POP3 VS IMAP

| Critère | SMTP | POP3 | IMAP |
|---------|------|------|------|
| Direction | Envoi | Réception | Réception/Gestion |
| Port standard | 25 / 587 | 110 | 143 |
| Port sécurisé | 465 | 995 | 993 |
| Stockage | Transit uniquement | Local après téléchargement | Sur le serveur |
| Multi-appareils | Non applicable | Limité | Natif |
| Gestion des dossiers | Non | Non | Oui |
| Hors ligne | Non | Oui après téléchargement | Partiel |
| Complexité | Moyenne | Faible | Élevée |
| Bande passante | Variable | Faible après réception | Plus élevée |
| Sécurité | TLS recommandé | TLS recommandé | TLS recommandé |
| Cas d'usage | Envoi | Utilisateur unique | Utilisateur moderne |

## Quand utiliser quel protocole ?

### Utiliser SMTP quand :

- Vous devez envoyer des emails
- Vous configurez un serveur de messagerie
- Vous développez une application qui envoie des notifications

### Utiliser POP3 quand :

- Vous utilisez un seul appareil
- Vous avez une connexion Internet limitée
- Vous souhaitez conserver une copie locale complète
- Vous voulez libérer de l'espace sur le serveur

### Utiliser IMAP quand :

- Vous utilisez plusieurs appareils
- Vous avez besoin de synchronisation
- Vous gérez de nombreux dossiers
- Vous accédez à vos emails via webmail et applications mobiles

---

# SÉCURITÉ DES PROTOCOLES EMAIL

## Menaces courantes

La messagerie électronique est une cible privilégiée pour les attaquants. Les menaces principales incluent :

- **Interception :** Lecture du contenu des messages en transit
- **Usurpation d'identité :** Envoi d'emails au nom d'autrui
- **Spam :** Envoi massif de messages non sollicités
- **Phishing :** Tromperie pour obtenir des informations sensibles
- **Malware :** Propagation de virus via pièces jointes
- **DDoS :** Attaques par déni de service sur les serveurs de messagerie
- **Replay attacks :** Réutilisation de sessions authentifiées

## Chiffrement

### TLS (Transport Layer Security)

TLS chiffre la connexion entre le client et le serveur. Il existe deux modes :

- **TLS implicite :** Connexion chiffrée dès le début (SMTPS, POP3S, IMAPS)
- **STARTTLS :** Connexion en clair suivie d'une mise à niveau TLS

### Configuration TLS recommandée

- Utiliser TLS 1.2 ou supérieur
- Désactiver SSLv2, SSLv3, TLS 1.0 et TLS 1.1
- Utiliser des certificats valides émis par une autorité de confiance
- Activer la vérification stricte des certificats
- Préférer des suites de chiffrement fortes (AES, ECDHE)

## Authentification

- Toujours exiger l'authentification pour l'envoi (SMTP AUTH)
- Utiliser des mots de passe forts et uniques
- Activer l'authentification multi-facteur (MFA) quand possible
- Utiliser des mécanismes sécurisés (CRAM-MD5, SCRAM, XOAUTH2)
- Ne jamais transmettre d'identifiants sans TLS

## SPF (Sender Policy Framework)

SPF permet à un domaine de déclarer quels serveurs sont autorisés à envoyer des emails en son nom.

### Exemple d'enregistrement SPF

```dns
example.com.    IN    TXT    "v=spf1 mx a:mail.example.com ip4:192.168.1.10 include:_spf.google.com ~all"
```

## DKIM (DomainKeys Identified Mail)

DKIM ajoute une signature cryptographique aux messages pour garantir leur authenticité et leur intégrité.

### Exemple d'enregistrement DKIM

```dns
selector._domainkey.example.com.    IN    TXT    "v=DKIM1; k=rsa; p=MIGfMA0GCSqG..."
```

## DMARC (Domain-based Message Authentication, Reporting, and Conformance)

DMARC combine SPF et DKIM et indique aux destinataires comment traiter les emails qui échouent aux vérifications.

### Exemple d'enregistrement DMARC

```dns
_dmarc.example.com.    IN    TXT    "v=DMARC1; p=quarantine; rua=mailto:dmarc@example.com; pct=100"
```

## MTA-STS (SMTP MTA Strict Transport Security)

MTA-STS force l'utilisation de TLS pour les communications SMTP entre serveurs.

### Exemple de politique MTA-STS

```
version: STSv1
mode: enforce
max_age: 604800
mx: mail.example.com
mx: backup.example.com
```

## DANE (DNS-based Authentication of Named Entities)

DANE utilise DNSSEC pour publier les certificats TLS des serveurs de messagerie.

---

# CONFIGURATION DES SERVEURS ET CLIENTS

## Configuration d'un serveur SMTP avec Postfix

### Installation sur Debian/Ubuntu

```bash
sudo apt update
sudo apt install postfix mailutils
```

### Fichier principal de configuration : /etc/postfix/main.cf

```ini
# Nom d'hôte du serveur
myhostname = mail.example.com

# Domaine principal
mydomain = example.com

# Origine par défaut des emails
myorigin = $mydomain

# Interfaces d'écoute
inet_interfaces = all
inet_protocols = ipv4

# Réseaux de confiance pour le relai
mynetworks = 127.0.0.0/8 [::ffff:127.0.0.0]/104 [::1]/128

# Destinations locales
mydestination = $myhostname, localhost.$mydomain, localhost, $mydomain

# Taille maximale des messages
message_size_limit = 20480000

# Limite de boîte aux lettres
mailbox_size_limit = 1073741824

# Authentification SASL
smtpd_sasl_type = dovecot
smtpd_sasl_path = private/auth
smtpd_sasl_auth_enable = yes
smtpd_sasl_security_options = noanonymous
smtpd_sasl_local_domain = $myhostname
broken_sasl_auth_clients = yes

# Restrictions
smtpd_recipient_restrictions =
    permit_mynetworks,
    permit_sasl_authenticated,
    reject_unauth_destination

# TLS
smtpd_tls_cert_file = /etc/letsencrypt/live/mail.example.com/fullchain.pem
smtpd_tls_key_file = /etc/letsencrypt/live/mail.example.com/privkey.pem
smtpd_tls_security_level = may
smtp_tls_security_level = may
smtpd_tls_loglevel = 1
```

### Fichier master.cf

```ini
#
# Postfix master process configuration file.
#
smtp      inet  n       -       y       -       -       smtpd
submission inet n       -       y       -       -       smtpd
  -o syslog_name=postfix/submission
  -o smtpd_tls_security_level=encrypt
  -o smtpd_tls_wrappermode=no
  -o smtpd_sasl_auth_enable=yes
  -o smtpd_sasl_type=dovecot
  -o smtpd_sasl_path=private/auth
  -o smtpd_sasl_security_options=noanonymous
  -o smtpd_sasl_local_domain=$myhostname
  -o smtpd_client_restrictions=permit_sasl_authenticated,reject
  -o smtpd_sender_restrictions=permit_sasl_authenticated
  -o smtpd_recipient_restrictions=permit_mynetworks,permit_sasl_authenticated,reject_unauth_destination
smtps     inet  n       -       y       -       -       smtpd
  -o syslog_name=postfix/smtps
  -o smtpd_tls_wrappermode=yes
  -o smtpd_sasl_auth_enable=yes
  -o smtpd_sasl_type=dovecot
  -o smtpd_sasl_path=private/auth
  -o smtpd_sasl_security_options=noanonymous
  -o smtpd_client_restrictions=permit_sasl_authenticated,reject
  -o smtpd_sender_restrictions=permit_sasl_authenticated
  -o smtpd_recipient_restrictions=permit_mynetworks,permit_sasl_authenticated,reject_unauth_destination
```

### Redémarrage de Postfix

```bash
sudo systemctl restart postfix
sudo postfix check
```

## Configuration d'un serveur POP3/IMAP avec Dovecot

### Installation sur Debian/Ubuntu

```bash
sudo apt install dovecot-core dovecot-imapd dovecot-pop3d
```

### Fichier /etc/dovecot/dovecot.conf

```ini
protocols = imap pop3 lmtp
listen = *, ::
```

### Fichier /etc/dovecot/conf.d/10-mail.conf

```ini
mail_location = maildir:~/Maildir
```

### Fichier /etc/dovecot/conf.d/10-auth.conf

```ini
disable_plaintext_auth = yes
auth_mechanisms = plain login
```

### Fichier /etc/dovecot/conf.d/10-ssl.conf

```ini
ssl = required
ssl_cert = </etc/letsencrypt/live/mail.example.com/fullchain.pem
ssl_key = </etc/letsencrypt/live/mail.example.com/privkey.pem
ssl_min_protocol = TLSv1.2
```

### Fichier /etc/dovecot/conf.d/10-master.conf

```ini
service auth {
  unix_listener /var/spool/postfix/private/auth {
    mode = 0666
    user = postfix
    group = postfix
  }
}
```

### Redémarrage de Dovecot

```bash
sudo systemctl restart dovecot
sudo dovecot -n
```

## Configuration d'un client email

### Paramètres généraux

| Paramètre | Valeur |
|-----------|--------|
| Serveur entrant IMAP | imap.example.com:993 (SSL/TLS) |
| Serveur entrant POP3 | pop.example.com:995 (SSL/TLS) |
| Serveur sortant SMTP | smtp.example.com:587 (STARTTLS) |
| Nom d'utilisateur | alice@example.com |
| Mot de passe | Votre mot de passe |

### Configuration de Thunderbird

1. Ouvrir Thunderbird
2. Menu ≡ > Nouveau > Compte existant
3. Saisir le nom, l'adresse email et le mot de passe
4. Choisir IMAP ou POP3
5. Vérifier les paramètres serveur
6. Valider

### Configuration d'Outlook

1. Fichier > Ajouter un compte
2. Saisir l'adresse email
3. Choisir Configuration manuelle
4. Sélectionner POP ou IMAP
5. Renseigner les serveurs entrant et sortant
6. Activer SSL/TLS
7. Tester les paramètres

### Configuration d'Apple Mail

1. Mail > Ajouter un compte
2. Choisir Autre compte de messagerie
3. Saisir le nom, l'adresse email et le mot de passe
4. Configurer les serveurs IMAP/POP3 et SMTP
5. Valider

---

# COMMANDES DE VÉRIFICATION SUR LINUX

## Vérification de la connectivité réseau

### Test d'un port SMTP avec netcat

```bash
nc -vz mail.example.com 25
nc -vz mail.example.com 587
nc -vz mail.example.com 465
```

### Test d'un port avec telnet

```bash
telnet mail.example.com 25
```

### Test avec curl

```bash
curl -v telnet://mail.example.com:25
curl -v telnet://mail.example.com:587
curl -v telnet://mail.example.com:993
```

## Vérification DNS

### Requête MX avec dig

```bash
dig MX example.com +short
dig MX example.com +trace
```

### Requête TXT (SPF, DKIM, DMARC)

```bash
dig TXT example.com +short
dig TXT _dmarc.example.com +short
dig TXT selector._domainkey.example.com +short
```

### Requête avec nslookup

```bash
nslookup -type=MX example.com
nslookup -type=TXT _dmarc.example.com
```

## Vérification SMTP en ligne de commande

### Test SMTP avec OpenSSL

```bash
# SMTP sur TLS (port 465)
openssl s_client -connect mail.example.com:465 -starttls smtp

# SMTP avec STARTTLS (port 587)
openssl s_client -connect mail.example.com:587 -starttls smtp

# SMTP standard (port 25)
openssl s_client -connect mail.example.com:25
```

### Envoi d'un email avec swaks

```bash
swaks --to bob@example.com \
      --from alice@example.com \
      --server mail.example.com \
      --auth LOGIN \
      --auth-user alice@example.com \
      --auth-password 'votre_mot_de_passe' \
      --tls \
      --header "Subject: Test avec swaks" \
      --body "Ceci est un message de test."
```

### Envoi avec mailx

```bash
echo "Corps du message" | mailx -s "Sujet du test" -S smtp=smtp://mail.example.com:587 -S smtp-auth=login -S smtp-auth-user=alice@example.com -S smtp-auth-password='votre_mot_de_passe' bob@example.com
```

## Vérification POP3 en ligne de commande

### Connexion POP3 avec OpenSSL

```bash
openssl s_client -connect mail.example.com:995
```

### Commandes POP3 manuelles

```pop3
USER alice
PASS secretpassword
STAT
LIST
RETR 1
QUIT
```

## Vérification IMAP en ligne de commande

### Connexion IMAP avec OpenSSL

```bash
openssl s_client -connect mail.example.com:993
```

### Commandes IMAP manuelles

```imap
a1 LOGIN alice secretpassword
a2 LIST "" "*"
a3 SELECT INBOX
a4 FETCH 1:* (FLAGS)
a5 LOGOUT
```

## Vérification des logs

### Logs Postfix

```bash
sudo tail -f /var/log/mail.log
sudo journalctl -u postfix -f
sudo postqueue -p
sudo postsuper -d ALL
```

### Logs Dovecot

```bash
sudo tail -f /var/log/mail.log
sudo journalctl -u dovecot -f
```

## Outils de test d'emails

### Vérification de la réputation d'un domaine

```bash
# Vérification de la présence sur des listes noires
dig +short 1.0.168.192.zen.spamhaus.org
```

### Analyse des en-têtes d'un email

```bash
# Afficher les en-têtes complets
cat email.eml | grep -E "^(Received|From|To|Subject|DKIM|SPF|DMARC)"
```

---

# COMMANDES DE VÉRIFICATION SUR WINDOWS

## Vérification de la connectivité réseau

### Test d'un port avec Test-NetConnection

```powershell
Test-NetConnection -ComputerName mail.example.com -Port 25
Test-NetConnection -ComputerName mail.example.com -Port 587
Test-NetConnection -ComputerName mail.example.com -Port 465
Test-NetConnection -ComputerName mail.example.com -Port 110
Test-NetConnection -ComputerName mail.example.com -Port 995
Test-NetConnection -ComputerName mail.example.com -Port 143
Test-NetConnection -ComputerName mail.example.com -Port 993
```

### Test avec telnet

```cmd
telnet mail.example.com 25
```

## Vérification DNS sur Windows

### Avec nslookup

```cmd
nslookup -type=MX example.com
nslookup -type=TXT example.com
nslookup -type=TXT _dmarc.example.com
```

### Avec Resolve-DnsName

```powershell
Resolve-DnsName -Name example.com -Type MX
Resolve-DnsName -Name example.com -Type TXT
Resolve-DnsName -Name _dmarc.example.com -Type TXT
```

## Vérification SMTP sur Windows

### Avec PowerShell

```powershell
$server = "mail.example.com"
$port = 587
$client = New-Object System.Net.Sockets.TcpClient
$client.Connect($server, $port)
$stream = $client.GetStream()
$writer = New-Object System.IO.StreamWriter($stream)
$reader = New-Object System.IO.StreamReader($stream)
$writer.AutoFlush = $true
$reader.ReadLine()
$writer.WriteLine("EHLO client")
while ($reader.Peek() -ne -1) { $reader.ReadLine() }
$writer.WriteLine("QUIT")
$reader.ReadLine()
$client.Close()
```

## Envoi d'email avec PowerShell

### Méthode simple avec Send-MailMessage

```powershell
Send-MailMessage -To "bob@example.com" `
                 -From "alice@example.com" `
                 -Subject "Test PowerShell" `
                 -Body "Ceci est un test." `
                 -SmtpServer "smtp.example.com" `
                 -Port 587 `
                 -UseSsl `
                 -Credential (Get-Credential)
```

### Méthode avec .NET MailMessage

```powershell
$smtp = New-Object Net.Mail.SmtpClient("smtp.example.com", 587)
$smtp.EnableSsl = $true
$smtp.Credentials = New-Object System.Net.NetworkCredential("alice@example.com", "votre_mot_de_passe")
$message = New-Object Net.Mail.MailMessage
$message.From = "alice@example.com"
$message.To.Add("bob@example.com")
$message.Subject = "Test avancé"
$message.Body = "Corps du message"
$smtp.Send($message)
```

## Vérification IMAP/POP3 sur Windows

### Avec OpenSSL pour Windows

```cmd
openssl s_client -connect mail.example.com:993
openssl s_client -connect mail.example.com:995
openssl s_client -connect mail.example.com:587 -starttls smtp
```

### Avec PowerShell et .NET

```powershell
# Test de connexion IMAP sur le port 993
Test-NetConnection -ComputerName mail.example.com -Port 993
```

---

# OPÉRATIONS PRATIQUES ET ENVOI DE MESSAGES

## Envoi d'un email via SMTP en ligne de commande

### Méthode Linux avec openssl

```bash
openssl s_client -connect smtp.gmail.com:587 -starttls smtp
```

Puis dans la session interactive :

```smtp
EHLO client
AUTH LOGIN
<base64 username>
<base64 password>
MAIL FROM:<alice@gmail.com>
RCPT TO:<bob@example.com>
DATA
Subject: Test manuel
From: alice@gmail.com
To: bob@example.com

Bonjour,
Ceci est un test envoyé manuellement.
.
QUIT
```

### Envoi avec Python

```python
import smtplib
from email.mime.text import MIMEText
from email.mime.multipart import MIMEMultipart

sender = "alice@example.com"
receiver = "bob@example.com"
password = "votre_mot_de_passe"

msg = MIMEMultipart()
msg['From'] = sender
msg['To'] = receiver
msg['Subject'] = "Test Python SMTP"

body = "Bonjour,\n\nCeci est un message envoyé avec Python."
msg.attach(MIMEText(body, 'plain'))

server = smtplib.SMTP('smtp.example.com', 587)
server.starttls()
server.login(sender, password)
text = msg.as_string()
server.sendmail(sender, receiver, text)
server.quit()
```

### Envoi avec pièce jointe en Python

```python
import smtplib
from email.mime.text import MIMEText
from email.mime.multipart import MIMEMultipart
from email.mime.base import MIMEBase
from email import encoders
import os

sender = "alice@example.com"
receiver = "bob@example.com"
password = "votre_mot_de_passe"

msg = MIMEMultipart()
msg['From'] = sender
msg['To'] = receiver
msg['Subject'] = "Test avec pièce jointe"

body = "Veuillez trouver ci-joint le fichier demandé."
msg.attach(MIMEText(body, 'plain'))

filename = "document.pdf"
attachment = open(filename, "rb")

part = MIMEBase('application', 'octet-stream')
part.set_payload(attachment.read())
encoders.encode_base64(part)
part.add_header('Content-Disposition', f"attachment; filename= {os.path.basename(filename)}")
msg.attach(part)

server = smtplib.SMTP('smtp.example.com', 587)
server.starttls()
server.login(sender, password)
server.sendmail(sender, receiver, msg.as_string())
server.quit()
```

### Envoi avec Node.js

```javascript
const nodemailer = require('nodemailer');

const transporter = nodemailer.createTransport({
  host: 'smtp.example.com',
  port: 587,
  secure: false,
  auth: {
    user: 'alice@example.com',
    pass: 'votre_mot_de_passe'
  }
});

const mailOptions = {
  from: 'alice@example.com',
  to: 'bob@example.com',
  subject: 'Test Node.js',
  text: 'Bonjour, ceci est un test avec Nodemailer.'
};

transporter.sendMail(mailOptions, (error, info) => {
  if (error) {
    console.log(error);
  } else {
    console.log('Email envoyé: ' + info.response);
  }
});
```

### Envoi avec PHP

```php
<?php
use PHPMailer\PHPMailer\PHPMailer;
use PHPMailer\PHPMailer\Exception;

require 'vendor/autoload.php';

$mail = new PHPMailer(true);

try {
    $mail->isSMTP();
    $mail->Host = 'smtp.example.com';
    $mail->SMTPAuth = true;
    $mail->Username = 'alice@example.com';
    $mail->Password = 'votre_mot_de_passe';
    $mail->SMTPSecure = 'tls';
    $mail->Port = 587;

    $mail->setFrom('alice@example.com', 'Alice');
    $mail->addAddress('bob@example.com', 'Bob');

    $mail->Subject = 'Test PHPMailer';
    $mail->Body = 'Ceci est un message de test envoyé avec PHPMailer.';

    $mail->send();
    echo 'Message envoyé avec succès';
} catch (Exception $e) {
    echo "Erreur: {$mail->ErrorInfo}";
}
?>
```

### Envoi avec Bash et mailutils

```bash
echo "Corps du message" | mail -s "Sujet" -a "From: alice@example.com" bob@example.com
```

## Récupération d'emails avec IMAP en Python

```python
import imaplib
import email

imap_server = "imap.example.com"
username = "alice@example.com"
password = "votre_mot_de_passe"

mail = imaplib.IMAP4_SSL(imap_server)
mail.login(username, password)
mail.select('inbox')

status, messages = mail.search(None, 'ALL')
message_ids = messages[0].split()

for msg_id in message_ids[-5:]:
    status, msg_data = mail.fetch(msg_id, '(RFC822)')
    raw_email = msg_data[0][1]
    email_message = email.message_from_bytes(raw_email)
    print(f"From: {email_message['From']}")
    print(f"Subject: {email_message['Subject']}")
    print(f"Date: {email_message['Date']}")
    print("---")

mail.close()
mail.logout()
```

## Récupération d'emails avec POP3 en Python

```python
import poplib
from email import parser

pop_server = "pop.example.com"
username = "alice@example.com"
password = "votre_mot_de_passe"

mailbox = poplib.POP3_SSL(pop_server)
mailbox.user(username)
mailbox.pass_(password)

num_messages = len(mailbox.list()[1])
print(f"Nombre de messages: {num_messages}")

for i in range(num_messages):
    raw_message = b"\n".join(mailbox.retr(i + 1)[1])
    parsed_message = parser.BytesParser().parsebytes(raw_message)
    print(f"Sujet: {parsed_message['Subject']}")
    print(f"De: {parsed_message['From']}")

mailbox.quit()
```

## Opérations de diagnostic

### Vérifier si un serveur accepte les relais

```bash
swaks --to test@example.com --from attacker@example.com --server cible.com --port 25
```

### Tester l'authentification SMTP

```bash
swaks --to bob@example.com --from alice@example.com --server mail.example.com --auth LOGIN --auth-user alice@example.com --auth-password 'pass'
```

### Vérifier les certificats TLS

```bash
openssl s_client -connect mail.example.com:993 -showcerts
openssl s_client -connect mail.example.com:995 -showcerts
openssl s_client -connect mail.example.com:587 -starttls smtp -showcerts
```

### Analyser les en-têtes d'un email

```bash
# Extraire les en-têtes Received
grep -E "^Received:" email.eml

# Vérifier les signatures DKIM
dkimverify < email.eml

# Vérifier SPF
dig TXT example.com +short
```

---

# APPLICATIONS ET LOGICIELS UTILISÉS

## Serveurs de messagerie

### Postfix

Postfix est un MTA libre, sécurisé et performant, très populaire sur Linux.

- **Site officiel :** https://www.postfix.org/
- **Auteur :** Wietse Venema
- **Licence :** IBM Public License / EPL
- **Plateformes :** Linux, Unix, macOS

### Sendmail

Sendmail est l'un des MTA les plus anciens. Très puissant mais complexe à configurer.

- **Site officiel :** https://www.proofpoint.com/us/products/email-protection/open-source-email-solution
- **Auteur :** Eric Allman
- **Licence :** Sendmail License

### Exim

Exim est un MTA flexible, utilisé notamment par Debian par défaut.

- **Site officiel :** https://www.exim.org/
- **Licence :** GPL

### Microsoft Exchange

Exchange est la solution de messagerie d'entreprise de Microsoft.

- **Site officiel :** https://www.microsoft.com/fr-fr/microsoft-365/exchange/email
- **Plateformes :** Windows Server

### Dovecot

Dovecot est un serveur IMAP et POP3 open source, rapide et sécurisé.

- **Site officiel :** https://www.dovecot.org/
- **Auteur :** Timo Sirainen
- **Licence :** MIT / LGPL

### Cyrus IMAP

Cyrus est un serveur IMAP conçu pour les environnements à grande échelle.

- **Site officiel :** https://www.cyrusimap.org/
- **Licence :** BSD

## Clients de messagerie

### Mozilla Thunderbird

Thunderbird est un client email libre et multiplateforme.

- **Site officiel :** https://www.thunderbird.net/
- **Licence :** MPL

### Microsoft Outlook

Outlook est le client email professionnel de Microsoft, intégré à Microsoft 365.

- **Site officiel :** https://www.microsoft.com/fr-fr/microsoft-365/outlook/email-and-calendar-software-microsoft-outlook

### Apple Mail

Apple Mail est le client email par défaut de macOS et iOS.

- **Site officiel :** https://www.apple.com/fr/macos/

### Evolution

Evolution est le client de messagerie du projet GNOME.

- **Site officiel :** https://wiki.gnome.org/Apps/Evolution

### Roundcube

Roundcube est un webmail open source moderne.

- **Site officiel :** https://roundcube.net/
- **Licence :** GPL

### Rainloop

Rainloop est un webmail léger et moderne.

- **Site officiel :** https://www.rainloop.net/

## Outils de test et diagnostic

| Outil | Description | Plateforme |
|-------|-------------|------------|
| swaks | Swiss Army Knife for SMTP | Linux |
| openssl | Tests TLS/SSL | Multiplateforme |
| dig / nslookup | Requêtes DNS | Linux/Windows |
| telnet | Connexion brute | Multiplateforme |
| curl | Transfert de données | Multiplateforme |
| mailx | Envoi d'emails en CLI | Linux |
| mxtoolbox.com | Diagnostic DNS/MX en ligne | Web |
| mail-tester.com | Test de réputation d'emails | Web |
| dmarcian.com | Analyse DMARC | Web |

---

# RESSOURCES, LIVRES ET LIENS

## RFC essentielles

| RFC | Titre | Date |
|-----|-------|------|
| RFC 821 | Simple Mail Transfer Protocol | 1982 |
| RFC 822 | Standard for the Format of ARPA Internet Text Messages | 1982 |
| RFC 1939 | Post Office Protocol - Version 3 | 1996 |
| RFC 2821 | Simple Mail Transfer Protocol (mise à jour) | 2001 |
| RFC 3501 | Internet Message Access Protocol - Version 4rev1 | 2003 |
| RFC 4408 | Sender Policy Framework | 2006 |
| RFC 4871 | DomainKeys Identified Mail (DKIM) | 2007 |
| RFC 5321 | Simple Mail Transfer Protocol | 2008 |
| RFC 5322 | Internet Message Format | 2008 |
| RFC 7208 | Sender Policy Framework (SPF) | 2014 |
| RFC 7489 | Domain-based Message Authentication, Reporting, and Conformance (DMARC) | 2015 |
| RFC 8461 | SMTP MTA Strict Transport Security (MTA-STS) | 2018 |
| RFC 9051 | Internet Message Access Protocol (IMAP) - Version 4rev2 | 2021 |

## Livres recommandés

- **"Postfix: The Definitive Guide"** - Kyle D. Dent
- **"The Book of Postfix"** - Ralf Hildebrandt, Patrick Koetter
- **"Sendmail"** - Bryan Costales, Eric Allman
- **"Email Security: How to Keep Your Email Safe"** - Various
- **"Learning Python Network Programming"** - Dr. M. O. Faruque Sarker, Sam Washington
- **"TCP/IP Illustrated, Volume 1"** - W. Richard Stevens
- **"The Internet Message"** - Marshall T. Rose
- **"Programming Internet Email"** - David Wood

## Sites web et documentation

- Postfix : https://www.postfix.org/documentation.html
- Dovecot : https://doc.dovecot.org/
- Exim : https://www.exim.org/docs.html
- Microsoft Exchange : https://docs.microsoft.com/fr-fr/exchange/
- Mozilla Thunderbird : https://support.mozilla.org/fr/products/thunderbird
- MX Toolbox : https://mxtoolbox.com/
- Mail Tester : https://www.mail-tester.com/
- Google Admin Toolbox : https://toolbox.googleapps.com/apps/checkmx/
- DMARC Analyzer : https://www.dmarcanalyzer.com/
- DKIM Core : https://dkimcore.org/

## Cours en ligne

- Coursera : "Internet History, Technology, and Security"
- Udemy : "Complete Mail Server Setup with Postfix, Dovecot and Roundcube"
- LinkedIn Learning : "Learning SMTP"
- Pluralsight : "Email Security Fundamentals"

## Communautés et forums

- Server Fault : https://serverfault.com/
- Stack Overflow : https://stackoverflow.com/
- Reddit r/sysadmin : https://www.reddit.com/r/sysadmin/
- Reddit r/email : https://www.reddit.com/r/email/
- Liste de diffusion Postfix : http://www.postfix.org/lists.html

---

# ANNEXES TECHNIQUES

## Annexe A : Table des ports réseau

| Protocole | Port | Description |
|-----------|------|-------------|
| SMTP      | 25   | Relai entre serveurs (souvent bloqué par les FAI) |
| SMTP      | 587  | Soumission authentifiée des emails (recommandé) |
| SMTPS     | 465  | SMTP sur SSL/TLS (désuet mais encore utilisé) |
| POP3      | 110  | POP3 en clair |
| POP3S     | 995  | POP3 sur SSL/TLS |
| IMAP      | 143  | IMAP en clair |
| IMAPS     | 993  | IMAP sur SSL/TLS |
| HTTP      | 80   | Webmail non sécurisé |
| HTTPS     | 443  | Webmail sécurisé |
| Sieve     | 4190 | Gestion des filtres de messagerie |
| LDAP      | 389  | Annuaire d'utilisateurs |
| LDAPS     | 636  | LDAP sécurisé |

## Annexe B : Codes d'erreur SMTP détaillés

### Erreurs temporaires (4xx)

| Code | Signification détaillée |
|------|-------------------------|
| 421  | Service non disponible, fermeture du canal |
| 450  | Boîte aux lettres indisponible (temporaire) |
| 451  | Erreur locale de traitement |
| 452  | Espace disque insuffisant |
| 455  | Serveur incapable de traiter les paramètres |

### Erreurs permanentes (5xx)

| Code | Signification détaillée |
|------|-------------------------|
| 500  | Erreur de syntaxe, commande non reconnue |
| 501  | Erreur de syntaxe dans les paramètres |
| 502  | Commande non implémentée |
| 503  | Mauvaise séquence de commandes |
| 504  | Paramètre de commande non implémenté |
| 550  | Boîte aux lettres indisponible |
| 551  | Utilisateur non local, essayer autre adresse |
| 552  | Message dépasse la taille maximale |
| 553  | Nom de boîte aux lettres incorrect |
| 554  | Transaction échouée |
| 555  | Paramètres MAIL FROM/RCPT TO non reconnus |

## Annexe C : Exemple complet d'enregistrements DNS pour un domaine email

```dns
; Enregistrements A
mail.example.com.        IN    A       192.168.1.10

; Enregistrements MX
example.com.             IN    MX      10 mail.example.com.
example.com.             IN    MX      20 backup.example.com.

; Enregistrement SPF
example.com.             IN    TXT     "v=spf1 mx a:mail.example.com ip4:192.168.1.10 ~all"

; Enregistrement DKIM
default._domainkey.example.com.    IN    TXT    "v=DKIM1; k=rsa; p=MIGfMA0GCSqGSIb3DQEBAQUAA4GNADCBiQKBgQC1TaNgLlSyQMNWVLNLvy/neHAha6HWKqgkJ9OlQgbWX/fLS7anAigPtsDZ6vi..."

; Enregistrement DMARC
_dmarc.example.com.      IN    TXT     "v=DMARC1; p=quarantine; rua=mailto:dmarc@example.com; ruf=mailto:forensic@example.com; pct=100; adkim=r; aspf=r"

; Enregistrement MTA-STS
_mta-sts.example.com.    IN    TXT     "v=STSv1; id=20260115120000;"

; Enregistrement TLS-RPT
_smtp._tls.example.com.  IN    TXT     "v=TLSRPTv1; rua=mailto:tls-reports@example.com"
```

## Annexe D : Fichiers de configuration avancés

### Configuration Postfix complète

```ini
# /etc/postfix/main.cf
# Générée par hackers_tchad - 2026

# Informations de base
myhostname = mail.example.com
mydomain = example.com
myorigin = $mydomain
inet_interfaces = all
inet_protocols = all
mydestination = $myhostname, localhost.$mydomain, localhost, $mydomain
mynetworks = 127.0.0.0/8 [::ffff:127.0.0.0]/104 [::1]/128

# Limites
message_size_limit = 52428800
mailbox_size_limit = 1073741824
smtpd_recipient_limit = 100
smtpd_hard_error_limit = 10

# Files d'attente
maximal_queue_lifetime = 5d
bounce_queue_lifetime = 5d

# SASL Authentication
smtpd_sasl_auth_enable = yes
smtpd_sasl_type = dovecot
smtpd_sasl_path = private/auth
smtpd_sasl_security_options = noanonymous, noplaintext
smtpd_sasl_tls_security_options = noanonymous
broken_sasl_auth_clients = yes
smtpd_sasl_local_domain = $myhostname

# TLS Configuration
smtpd_tls_cert_file = /etc/letsencrypt/live/mail.example.com/fullchain.pem
smtpd_tls_key_file = /etc/letsencrypt/live/mail.example.com/privkey.pem
smtpd_tls_CAfile = /etc/letsencrypt/live/mail.example.com/chain.pem
smtpd_use_tls = yes
smtpd_tls_security_level = may
smtp_tls_security_level = may
smtpd_tls_loglevel = 1
smtpd_tls_received_header = yes
smtpd_tls_session_cache_timeout = 3600s
smtp_tls_note_starttls_offer = yes

# Restrictions
smtpd_helo_required = yes
smtpd_delay_reject = yes
smtpd_helo_restrictions = permit_mynetworks, reject_invalid_helo_hostname, reject_non_fqdn_helo_hostname
smtpd_sender_restrictions = permit_mynetworks, reject_non_fqdn_sender, reject_unknown_sender_domain
smtpd_recipient_restrictions =
    permit_mynetworks,
    permit_sasl_authenticated,
    reject_unauth_destination,
    reject_non_fqdn_recipient,
    reject_unknown_recipient_domain,
    reject_rbl_client zen.spamhaus.org,
    reject_rbl_client bl.spamcop.net

# Anti-spam
smtpd_data_restrictions = reject_unauth_pipelining
header_checks = regexp:/etc/postfix/header_checks
body_checks = regexp:/etc/postfix/body_checks
```

### Configuration Dovecot complète

```ini
# /etc/dovecot/dovecot.conf
protocols = imap pop3 lmtp sieve
listen = *, ::
base_dir = /var/run/dovecot/
login_greeting = Dovecot ready.

# /etc/dovecot/conf.d/10-mail.conf
mail_location = maildir:~/Maildir
mail_uid = vmail
mail_gid = vmail
mail_privileged_group = mail
first_valid_uid = 1000
last_valid_uid = 0

# /etc/dovecot/conf.d/10-auth.conf
disable_plaintext_auth = yes
auth_mechanisms = plain login
!include auth-system.conf.ext

# /etc/dovecot/conf.d/10-ssl.conf
ssl = required
ssl_cert = </etc/letsencrypt/live/mail.example.com/fullchain.pem
ssl_key = </etc/letsencrypt/live/mail.example.com/privkey.pem
ssl_min_protocol = TLSv1.2
ssl_prefer_server_ciphers = yes
ssl_cipher_list = ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES256-GCM-SHA384

# /etc/dovecot/conf.d/20-imap.conf
protocol imap {
    mail_max_userip_connections = 30
    mail_plugins = $mail_plugins imap_quota
}

# /etc/dovecot/conf.d/20-pop3.conf
protocol pop3 {
    pop3_uidl_format = %08Xu%08Xv
    mail_max_userip_connections = 10
}

# /etc/dovecot/conf.d/10-master.conf
service imap-login {
    inet_listener imap {
        port = 143
    }
    inet_listener imaps {
        port = 993
        ssl = yes
    }
}

service pop3-login {
    inet_listener pop3 {
        port = 110
    }
    inet_listener pop3s {
        port = 995
        ssl = yes
    }
}

service auth {
    unix_listener /var/spool/postfix/private/auth {
        mode = 0666
        user = postfix
        group = postfix
    }
    unix_listener auth-userdb {
        mode = 0600
        user = vmail
    }
}

service lmtp {
    unix_listener /var/spool/postfix/private/dovecot-lmtp {
        mode = 0600
        user = postfix
        group = postfix
    }
}
```

## Annexe E : Scripts d'administration

### Script de surveillance de la file d'attente Postfix

```bash
#!/bin/bash
# Script : check_postfix_queue.sh
# Auteur : hackers_tchad
# Date : 2026

LIMIT=100
QUEUE_COUNT=$(mailq | tail -n 1 | awk '{print $5}')

if [ -z "$QUEUE_COUNT" ]; then
    QUEUE_COUNT=0
fi

if [ "$QUEUE_COUNT" -gt "$LIMIT" ]; then
    echo "ALERTE: $QUEUE_COUNT messages en attente dans la file Postfix"
    echo "Voir les détails avec: postqueue -p"
    exit 1
else
    echo "OK: $QUEUE_COUNT messages en attente"
    exit 0
fi
```

### Script de test IMAP avec Python

```python
#!/usr/bin/env python3
# Script : test_imap.py
# Auteur : hackers_tchad
# Date : 2026

import imaplib
import sys

HOST = sys.argv[1] if len(sys.argv) > 1 else 'localhost'
USER = sys.argv[2] if len(sys.argv) > 2 else 'test@example.com'
PASS = sys.argv[3] if len(sys.argv) > 3 else 'password'

try:
    mail = imaplib.IMAP4_SSL(HOST)
    mail.login(USER, PASS)
    status, messages = mail.select('INBOX')
    print(f"Connexion IMAP réussie. Messages dans INBOX: {messages[0].decode()}")
    mail.logout()
except Exception as e:
    print(f"Erreur IMAP: {e}")
    sys.exit(1)
```

### Script de test SMTP avec Python

```python
#!/usr/bin/env python3
# Script : test_smtp.py
# Auteur : hackers_tchad
# Date : 2026

import smtplib
import sys

HOST = sys.argv[1] if len(sys.argv) > 1 else 'localhost'
PORT = int(sys.argv[2]) if len(sys.argv) > 2 else 587
USER = sys.argv[3] if len(sys.argv) > 3 else 'test@example.com'
PASS = sys.argv[4] if len(sys.argv) > 4 else 'password'
TO = sys.argv[5] if len(sys.argv) > 5 else USER

try:
    server = smtplib.SMTP(HOST, PORT)
    server.starttls()
    server.login(USER, PASS)
    server.sendmail(USER, [TO], f"Subject: Test SMTP\n\nCeci est un test.")
    server.quit()
    print("Email envoyé avec succès")
except Exception as e:
    print(f"Erreur SMTP: {e}")
    sys.exit(1)
```

---

# GLOSSAIRE

| Terme | Définition |
|-------|------------|
| **ARPA** | Advanced Research Projects Agency |
| **ARPANET** | Réseau expérimental précurseur d'Internet |
| **Base64** | Encodage utilisé pour transformer des données binaires en texte ASCII |
| **BCC** | Blind Carbon Copy, copie cachée |
| **CC** | Carbon Copy, copie conforme |
| **DKIM** | Signature cryptographique des messages |
| **DMARC** | Politique d'authentification des emails |
| **DNS** | Système de noms de domaine |
| **ESMTP** | SMTP étendu avec des fonctionnalités supplémentaires |
| **IMAP** | Protocole d'accès aux messages sur serveur |
| **MUA** | Mail User Agent, client email |
| **MTA** | Mail Transfer Agent, serveur de transfert |
| **MDA** | Mail Delivery Agent, agent de livraison |
| **MX** | Mail Exchanger, enregistrement DNS |
| **POP3** | Protocole de récupération d'emails |
| **RFC** | Request for Comments, document de standardisation |
| **SMTP** | Protocole de transfert de courrier |
| **SPF** | Framework de politique d'expéditeur |
| **STARTTLS** | Commande pour activer TLS sur une connexion existante |
| **TLS** | Transport Layer Security, protocole de chiffrement |
| **UID** | Unique Identifier, identifiant unique d'un message IMAP |
| **Webmail** | Interface web d'accès aux emails |

---

# FAQ

## Quelle est la différence entre POP3 et IMAP ?

POP3 télécharge les emails sur un appareil local et les supprime généralement du serveur. IMAP conserve les messages sur le serveur et synchronise l'état entre plusieurs appareils.

## Pourquoi le port 25 est-il souvent bloqué ?

Le port 25 est fréquemment bloqué par les fournisseurs d'accès pour lutter contre le spam et les serveurs ouverts. Les clients doivent utiliser le port 587 avec authentification.

## Que signifie STARTTLS ?

STARTTLS est une commande permettant de transformer une connexion non chiffrée en connexion chiffrée avec TLS.

## Comment vérifier si mon serveur email est sur une liste noire ?

Vous pouvez utiliser des services en ligne comme MX Toolbox, Spamhaus ou Barracuda Reputation pour vérifier la réputation de votre adresse IP.

## Qu'est-ce qu'un enregistrement MX ?

Un enregistrement MX indique quel serveur de messagerie est responsable de la réception des emails pour un domaine.

## Pourquoi utiliser DMARC ?

DMARC permet de protéger un domaine contre l'usurpation en indiquant aux serveurs destinataires comment traiter les emails qui échouent aux vérifications SPF et DKIM.

## Comment sécuriser un serveur SMTP ?

- Exiger l'authentification pour l'envoi
- Activer TLS/STARTTLS
- Configurer SPF, DKIM et DMARC
- Limiter les réseaux de confiance
- Surveiller les logs
- Mettre à jour régulièrement le logiciel

---

# DÉPANNAGE ET TROUBLESHOOTING

## Problème : Impossible d'envoyer des emails

### Causes possibles

- Port SMTP bloqué par le pare-feu ou le FAI
- Authentification incorrecte
- Certificat TLS invalide
- Serveur sur liste noire
- Destinataire inexistant

### Solutions

```bash
# Vérifier la connectivité
nc -vz smtp.example.com 587

# Vérifier l'authentification avec swaks
swaks --to test@example.com --from alice@example.com --server smtp.example.com --auth LOGIN --auth-user alice@example.com --tls

# Consulter les logs
sudo tail -f /var/log/mail.log
```

## Problème : Impossible de recevoir des emails

### Causes possibles

- Enregistrement MX incorrect ou manquant
- Serveur de messagerie arrêté
- Port 25 bloqué
- Boîte aux lettres pleine
- Règles de filtrage trop strictes

### Solutions

```bash
# Vérifier les enregistrements MX
dig MX example.com +short

# Vérifier l'état du serveur
sudo systemctl status postfix
sudo systemctl status dovecot

# Vérifier l'espace disque
df -h
```

## Problème : Erreur de certificat TLS

### Causes possibles

- Certificat expiré
- Nom de domaine incorrect
- Autorité de certification non reconnue

### Solutions

```bash
# Vérifier le certificat
openssl s_client -connect mail.example.com:993 -showcerts

# Vérifier la date d'expiration
openssl x509 -in /etc/letsencrypt/live/mail.example.com/cert.pem -noout -dates
```

## Problème : Emails marqués comme spam

### Causes possibles

- SPF, DKIM ou DMARC mal configurés
- IP sur liste noire
- Contenu suspect
- Taux de plaintes élevé

### Solutions

- Vérifier les enregistrements DNS
- Configurer correctement SPF, DKIM et DMARC
- Utiliser des IPs dédiées et réputées
- Respecter les bonnes pratiques d'envoi

---

# BONNES PRATIQUES

## Sécurité

1. Toujours utiliser TLS pour les connexions client-serveur et serveur-serveur.
2. Exiger l'authentification SMTP pour tous les envois.
3. Implémenter SPF, DKIM et DMARC.
4. Surveiller les logs et les tentatives d'accès.
5. Limiter les tentatives de connexion pour prévenir les attaques par force brute.
6. Mettre à jour régulièrement les logiciels.
7. Utiliser des mots de passe forts et de l'authentification multi-facteur.

## Performance

1. Limiter la taille maximale des messages.
2. Utiliser des files d'attente adaptées.
3. Activer le pipelining SMTP.
4. Optimiser les requêtes DNS.
5. Surveiller l'utilisation des ressources.

## Fiabilité

1. Configurer des serveurs de messagerie secondaires (MX secondaires).
2. Sauvegarder régulièrement les boîtes aux lettres.
3. Mettre en place une supervision proactive.
4. Tester régulièrement les procédures de récupération.

## Conformité

1. Respecter les lois anti-spam (CAN-SPAM, GDPR, etc.).
2. Fournir une option de désinscription claire.
3. Ne pas acheter de listes d'adresses.
4. Protéger les données personnelles des utilisateurs.

---

# CONCLUSION

Les protocoles SMTP, POP3 et IMAP forment le socle de la messagerie électronique moderne. Bien qu'ils aient été conçus il y a plusieurs décennies, ils ont évolué pour répondre aux exigences actuelles en matière de sécurité, de performance et d'accessibilité.

SMTP reste le protocole incontournable pour l'envoi de messages. POP3, bien que moins utilisé dans les environnements modernes, conserve son intérêt pour les besoins spécifiques de récupération locale. IMAP s'est imposé comme le standard de facto pour l'accès multi-appareils et la gestion avancée des emails.

La sécurisation de ces protocoles passe par l'utilisation systématique de TLS, l'authentification forte, la mise en œuvre de SPF, DKIM et DMARC, ainsi qu'une surveillance régulière des serveurs.

Ce guide a couvert de manière approfondie les principes fondamentaux, les configurations, les commandes de vérification, les opérations pratiques et les ressources complémentaires. Il constitue une référence pour tout administrateur, développeur ou passionné souhaitant maîtriser la messagerie électronique.

---

## Résumé des points clés

- **SMTP :** Envoi et transfert d'emails (ports 25, 587, 465)
- **POP3 :** Récupération simple avec stockage local (ports 110, 995)
- **IMAP :** Gestion avancée sur serveur avec synchronisation (ports 143, 993)
- **Sécurité :** TLS, authentification, SPF, DKIM, DMARC, MTA-STS
- **Outils :** Postfix, Dovecot, swaks, openssl, dig, Thunderbird, Outlook
- **Auteur :** hackers_tchad
- **Date :** 2026

---

## Remerciements

Ce document a été rédigé par `hackers_tchad` dans un but éducatif et technique. Les informations présentées sont basées sur les RFC officielles, la documentation des logiciels mentionnés et les bonnes pratiques reconnues par la communauté.

---

**Fin du document**

*Document généré en 2026 par hackers_tchad. Tous droits réservés sur le contenu original.*
