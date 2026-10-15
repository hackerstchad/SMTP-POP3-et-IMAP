# Protocoles de Messagerie Électronique : SMTP, POP3 et IMAP

**Auteur :** hackers_tchad  
**Date de publication :** 2026  
**Version :** 1.0 - Édition Avancée  
**Licence :** Documentation éducative et technique libre

---

## Table des matières

1. [Introduction générale](#introduction-générale)
2. [Historique et créateurs](#historique-et-créateurs)
3. [Architecture globale de la messagerie](#architecture-globale-de-la-messagerie)
4. [SMTP - Simple Mail Transfer Protocol](#smtp---simple-mail-transfer-protocol)
   - 4.1. Définition et rôle
   - 4.2. Historique
   - 4.3. Architecture SMTP
   - 4.4. Fonctionnement détaillé
   - 4.5. Commandes SMTP
   - 4.6. Codes de réponse SMTP
   - 4.7. Ports et sécurité
   - 4.8. Configuration SMTP
   - 4.9. Vérification et tests sous Linux
   - 4.10. Vérification et tests sous Windows
   - 4.11. Envoi d'un email manuellement
   - 4.12. En-têtes SMTP
   - 4.13. SPF, DKIM, DMARC
   - 4.14. SMTP Auth et Relay
   - 4.15. Dépannage SMTP
5. [POP3 - Post Office Protocol v3](#pop3---post-office-protocol-v3)
   - 5.1. Définition et rôle
   - 5.2. Historique
   - 5.3. Architecture POP3
   - 5.4. Fonctionnement détaillé
   - 5.5. Commandes POP3
   - 5.6. États de session POP3
   - 5.7. Ports et sécurité
   - 5.8. Configuration POP3
   - 5.9. Vérification et tests sous Linux
   - 5.10. Vérification et tests sous Windows
   - 5.11. Récupération manuelle d'emails
   - 5.12. Dépannage POP3
6. [IMAP - Internet Message Access Protocol](#imap---internet-message-access-protocol)
   - 6.1. Définition et rôle
   - 6.2. Historique
   - 6.3. Architecture IMAP
   - 6.4. Fonctionnement détaillé
   - 6.5. Commandes IMAP
   - 6.6. États de session IMAP
   - 6.7. Ports et sécurité
   - 6.8. Configuration IMAP
   - 6.9. Vérification et tests sous Linux
   - 6.10. Vérification et tests sous Windows
   - 6.11. Manipulation manuelle de boîtes IMAP
   - 6.12. Dépannage IMAP
7. [Comparatif SMTP / POP3 / IMAP](#comparatif-smtp--pop3--imap)
8. [Où et comment sont utilisés ces protocoles](#où-et-comment-sont-utilisés-ces-protocoles)
9. [Applications et logiciels utilisant ces protocoles](#applications-et-logiciels-utilisant-ces-protocoles)
10. [Configuration sur les principaux serveurs](#configuration-sur-les-principaux-serveurs)
11. [Sécurité de la messagerie](#sécurité-de-la-messagerie)
12. [Commandes de vérification réseau](#commandes-de-vérification-réseau)
13. [Exercices pratiques](#exercices-pratiques)
14. [Ressources, livres et liens](#ressources-livres-et-liens)
15. [Glossaire](#glossaire)
16. [Conclusion](#conclusion)

---

## Introduction générale

La messagerie électronique est l'un des services les plus anciens et les plus utilisés d'Internet. Elle repose sur un ensemble de protocoles standardisés qui permettent d'envoyer, de recevoir, de stocker et de consulter des messages électroniques. Les trois protocoles fondamentaux de la messagerie sont le **SMTP (Simple Mail Transfer Protocol)**, le **POP3 (Post Office Protocol version 3)** et l'**IMAP (Internet Message Access Protocol)**.

Ces protocoles ont été conçus à des époques différentes, pour répondre à des besoins variés, et ils continuent d'évoluer pour s'adapter aux exigences modernes de sécurité, de mobilité et de performance. SMTP est le protocole d'envoi, tandis que POP3 et IMAP sont les protocoles de réception et de consultation.

Dans ce document, nous allons explorer en profondeur chacun de ces protocoles, leur histoire, leur architecture, leur configuration, les commandes de vérification sous Linux et Windows, ainsi que les bonnes pratiques de sécurité. Nous verrons également comment effectuer des opérations manuelles, comment envoyer et recevoir des emails, et comment diagnostiquer les problèmes courants.

Ce guide s'adresse aux administrateurs système, aux ingénieurs réseau, aux étudiants en informatique, aux professionnels de la cybersécurité et à toute personne souhaitant maîtriser les rouages de la messagerie électronique.

---

## Historique et créateurs

### SMTP

Le protocole SMTP a été défini pour la première fois dans la RFC 821 en 1982 par **Jonathan B. Postel**, un pionnier d'Internet. Postel travaillait à l'Institute for Computer Sciences (ISI) de l'University of Southern California (USC) et a contribué à de nombreux protocoles fondamentaux d'Internet. SMTP a été conçu pour remplacer le protocole FTP Mail (en utilisant la commande `MAIL`), qui était utilisé à l'époque pour le transfert de messages.

La version actuelle de SMTP est décrite dans la RFC 5321 (2008), qui met à jour les spécifications antérieures. SMTP est un protocole de la couche application du modèle OSI, utilisant TCP comme protocole de transport.

### POP3

Le protocole POP a été développé pour permettre aux utilisateurs de récupérer leur courrier depuis un serveur central. La première version, POP1, a été décrite dans la RFC 918 en 1984. POP2 a suivi dans la RFC 937 en 1985. Cependant, c'est la version 3, définie dans la RFC 1081 en 1988, puis standardisée dans la RFC 1939 en 1996, qui est la plus utilisée aujourd'hui.

Les principaux contributeurs au développement de POP incluent **Marshall T. Rose**, **John G. Myers** et de nombreux membres de la communauté Internet. POP3 a été conçu dans un contexte où les utilisateurs se connectaient temporairement à Internet via des modems, téléchargeaient leurs emails sur un seul ordinateur, puis se déconnectaient.

### IMAP

IMAP a été développé comme une alternative plus avancée à POP. Il a été créé par **Mark Crispin** en 1986 alors qu'il travaillait au Stanford Knowledge Systems Laboratory. La première version expérimentale a été décrite dans la RFC 1064 en 1988, et IMAP2 dans la RFC 1176 en 1990. IMAP4, la version actuelle, est définie dans la RFC 1730 (1994) et ses révisions dans la RFC 2060 (1996), RFC 3501 (2003) et RFC 9051 (2021).

Mark Crispin a conçu IMAP pour permettre une gestion avancée des boîtes aux lettres directement sur le serveur, facilitant l'accès depuis plusieurs appareils et la synchronisation des messages.

---

## Architecture globale de la messagerie

L'architecture de la messagerie électronique repose sur plusieurs composants interdépendants :

1. **MUA (Mail User Agent)** : Le client de messagerie utilisé par l'utilisateur final. Exemples : Thunderbird, Outlook, Apple Mail, webmails.
2. **MTA (Mail Transfer Agent)** : Le serveur qui transfère les emails d'un serveur à un autre. Exemples : Postfix, Sendmail, Exim, Microsoft Exchange.
3. **MDA (Mail Delivery Agent)** : Le composant responsable de la livraison des emails dans la boîte aux lettres de l'utilisateur. Exemples : Dovecot LDA, Procmail, Maildrop.
4. **MRA (Mail Retrieval Agent)** : Le serveur qui permet aux clients de récupérer leurs emails. POP3 et IMAP jouent ce rôle.
5. **DNS (Domain Name System)** : Utilisé pour résoudre les enregistrements MX (Mail Exchanger) et diriger les emails vers les bons serveurs.
6. **Boîtes aux lettres (Mailboxes)** : Espaces de stockage des messages sur le serveur, généralement au format mbox ou Maildir.

### Flux d'un email

Lorsqu'un utilisateur envoie un email, le parcours typique est le suivant :

1. L'utilisateur rédige un message dans son MUA (client de messagerie).
2. Le MUA envoie le message au serveur SMTP sortant (MTA) de son fournisseur.
3. Le MTA source consulte les enregistrements MX du domaine destinataire via le DNS.
4. Le MTA source établit une connexion SMTP avec le MTA destination.
5. Le MTA destination accepte le message et le confie à un MDA.
6. Le MDA stocke le message dans la boîte aux lettres du destinataire.
7. Le destinataire utilise un client POP3 ou IMAP pour consulter ou télécharger ses messages.

Cette architecture distribuée garantit la robustesse, la scalabilité et l'interopérabilité de la messagerie sur Internet.

---

## SMTP - Simple Mail Transfer Protocol

### 4.1. Définition et rôle

SMTP, ou Simple Mail Transfer Protocol, est le protocole standard utilisé pour l'envoi et le transfert de courriers électroniques sur Internet. Il opère principalement en mode push : il pousse les emails du client vers le serveur, puis d'un serveur à un autre, jusqu'à atteindre le serveur de destination.

SMTP est un protocole textuel, orienté connexion, utilisant TCP. Il est relativement simple dans sa conception initiale, mais il a été enrichi au fil des années pour supporter l'authentification, le chiffrement TLS, les pièces jointes encodées en MIME, et les mécanismes de lutte contre le spam.

### 4.2. Historique

- 1971 : Premiers systèmes de messagerie sur ARPANET utilisant des commandes simples.
- 1973 : Standardisation des adresses email au format `utilisateur@hôte`.
- 1980 : Utilisation de FTP pour transférer les messages (`MAIL`).
- 1982 : Publication de la RFC 821 par Jonathan Postel, définissant SMTP.
- 1984 : Extension MIME dans les RFC 2045-2049 pour les pièces jointes.
- 1995 : Introduction de ESMTP (Extended SMTP) dans la RFC 1869.
- 1999 : SMTP AUTH dans la RFC 2554 pour l'authentification.
- 2002 : SMTP over TLS dans la RFC 3207 (STARTTLS).
- 2008 : RFC 5321, version actuelle de SMTP.
- 2018-2024 : Renforcement des exigences SPF, DKIM, DMARC et MTA-STS.

### 4.3. Architecture SMTP

L'architecture SMTP repose sur deux entités principales :

- **Client SMTP (SMTP Client)** : Envoie les messages, par exemple le MUA de l'utilisateur ou un MTA relayant un message.
- **Serveur SMTP (SMTP Server)** : Reçoit les messages, par exemple le serveur entrant d'un domaine ou le serveur sortant d'un FAI.

Les serveurs SMTP communiquent entre eux pour acheminer les messages. Le DNS fournit les enregistrements MX qui indiquent quels serveurs sont responsables de la réception des emails pour un domaine donné.

### 4.4. Fonctionnement détaillé

Une session SMTP typique suit la séquence suivante :

1. Le client établit une connexion TCP sur le port 25, 587 ou 465 du serveur.
2. Le serveur répond avec un code de bienvenue (greeting).
3. Le client envoie la commande `EHLO` (ou `HELO` pour les anciens serveurs).
4. Le serveur répond avec ses capacités (ESMTP).
5. Le client s'authentifie si nécessaire (`AUTH LOGIN` ou `AUTH PLAIN`).
6. Le client indique l'expéditeur avec `MAIL FROM:`.
7. Le client indique le destinataire avec `RCPT TO:`.
8. Le client envoie la commande `DATA`.
9. Le client transmet le contenu du message (en-têtes et corps), terminé par une ligne contenant uniquement un point.
10. Le serveur confirme la réception avec un code de réponse.
11. Le client termine la session avec `QUIT`.

### 4.5. Commandes SMTP

Voici les principales commandes SMTP :

- `HELO nom_client` : Salutation initiale (SMTP simple).
- `EHLO nom_client` : Salutation étendue (ESMTP).
- `MAIL FROM:<adresse>` : Spécifie l'expéditeur.
- `RCPT TO:<adresse>` : Spécifie le destinataire.
- `DATA` : Indique le début du corps du message.
- `RSET` : Réinitialise la transaction en cours.
- `VRFY` : Vérifie une adresse email (souvent désactivé).
- `EXPN` : Développe une liste de distribution (souvent désactivé).
- `HELP` : Affiche l'aide.
- `QUIT` : Termine la session.
- `NOOP` : Commande vide, utilisée pour maintenir la connexion.
- `AUTH` : Authentifie le client (ESMTP).
- `STARTTLS` : Passe la connexion en TLS (ESMTP).
- `SIZE` : Indique la taille maximale acceptée.
- `PIPELINING` : Permet d'envoyer plusieurs commandes d'affilée.
- `8BITMIME` : Support des caractères 8 bits.

### 4.6. Codes de réponse SMTP

Les codes de réponse SMTP sont constitués de trois chiffres :

- **2xx** : Succès
  - `220` : Service prêt
  - `221` : Fermeture du canal de transmission
  - `235` : Authentification réussie
  - `250` : Action demandée effectuée avec succès
  - `251` : Utilisateur non local, message transféré
  - `252` : Impossible de vérifier l'utilisateur, message accepté
- **3xx** : Redirection ou continuation
  - `334` : Réponse de l'authentification (challenge)
  - `354` : Début du message, terminez par `<CRLF>.<CRLF>`
- **4xx** : Erreur temporaire
  - `421` : Service non disponible, fermeture du canal
  - `450` : Action non effectuée, boîte aux lettres occupée
  - `451` : Erreur locale de traitement
  - `452` : Espace insuffisant
  - `454` : Authentification temporairement indisponible
- **5xx** : Erreur permanente
  - `500` : Erreur de syntaxe, commande non reconnue
  - `501` : Erreur de syntaxe dans les paramètres
  - `502` : Commande non implémentée
  - `503` : Mauvaise séquence de commandes
  - `530` : Authentification requise
  - `535` : Échec de l'authentification
  - `550` : Boîte aux lettres indisponible
  - `551` : Utilisateur non local
  - `552` : Dépassement de quota
  - `553` : Nom de boîte aux lettres incorrect
  - `554` : Transaction échouée

### 4.7. Ports et sécurité

Les ports utilisés par SMTP sont :

- **Port 25** : Port historique pour le transfert de messages entre MTA (souvent bloqué par les FAI pour les clients afin de lutter contre le spam).
- **Port 587** : Port recommandé pour la soumission des emails par les clients (submission), avec authentification et TLS.
- **Port 465** : Port SMTPS, utilisé historiquement pour SMTP sur SSL/TLS. Réhabilité par la RFC 8314 pour la soumission avec TLS implicite.
- **Port 2525** : Port alternatif parfois utilisé lorsque le port 25 est bloqué.

Il est recommandé d'utiliser le port 587 avec STARTTLS ou le port 465 avec TLS implicite pour l'envoi depuis un MUA. Le port 25 reste principalement réservé au trafic inter-serveur.

### 4.8. Configuration SMTP

#### Configuration d'un client SMTP

Les paramètres typiques d'un client SMTP sont :

- **Serveur SMTP** : `smtp.fournisseur.com`
- **Port** : `587` (STARTTLS) ou `465` (TLS/SSL)
- **Méthode de chiffrement** : STARTTLS ou SSL/TLS
- **Authentification** : Oui, avec nom d'utilisateur et mot de passe
- **Nom d'utilisateur** : L'adresse email complète
- **Mot de passe** : Le mot de passe du compte email

#### Configuration de Postfix (exemple)

Postfix est l'un des MTA les plus populaires sous Linux. Voici un exemple de configuration minimale dans `/etc/postfix/main.cf` :

```ini
myhostname = mail.example.com
mydomain = example.com
myorigin = $mydomain
inet_interfaces = all
mydestination = $myhostname, localhost.$mydomain, localhost, $mydomain
mynetworks = 127.0.0.0/8 [::ffff:127.0.0.0]/104 [::1]/128
home_mailbox = Maildir/
smtpd_banner = $myhostname ESMTP
smtpd_tls_security_level = may
smtp_tls_security_level = may
smtpd_tls_cert_file = /etc/ssl/certs/postfix.pem
smtpd_tls_key_file = /etc/ssl/private/postfix.key
smtpd_sasl_auth_enable = yes
smtpd_sasl_type = dovecot
smtpd_sasl_path = private/auth
smtpd_recipient_restrictions = permit_mynetworks, permit_sasl_authenticated, reject_unauth_destination
```

Après modification, recharger la configuration avec :

```bash
sudo postfix reload
```

### 4.9. Vérification et tests sous Linux

#### Vérifier que le service SMTP écoute

```bash
sudo ss -tlnp | grep -E ':25|:587|:465'
```

#### Tester un serveur SMTP avec telnet

```bash
telnet smtp.example.com 587
```

Puis, dans la session interactive :

```
EHLO client.example.com
MAIL FROM:<expediteur@example.com>
RCPT TO:<destinataire@example.com>
DATA
Subject: Test SMTP

Ceci est un test.
.
QUIT
```

#### Tester avec OpenSSL (TLS implicite sur le port 465)

```bash
openssl s_client -connect smtp.example.com:465 -starttls smtp
```

Pour STARTTLS sur le port 587 :

```bash
openssl s_client -starttls smtp -connect smtp.example.com:587
```

#### Vérifier les enregistrements MX

```bash
dig MX example.com
```

ou

```bash
nslookup -type=MX example.com
```

#### Tester l'envoi avec swaks

`swaks` est un outil puissant pour tester SMTP :

```bash
swaks --to destinataire@example.com --from expediteur@example.com --server smtp.example.com --auth-user expediteur@example.com --auth-password "motdepasse" --tls
```

#### Vérifier les logs SMTP

Sous Debian/Ubuntu avec Postfix :

```bash
sudo tail -f /var/log/mail.log
```

Sous RHEL/CentOS/Rocky Linux :

```bash
sudo tail -f /var/log/maillog
```

#### Vérifier la file d'attente

```bash
sudo postqueue -p
sudo postsuper -d ALL
```

### 4.10. Vérification et tests sous Windows

#### Tester un serveur SMTP avec PowerShell

```powershell
Test-NetConnection -ComputerName smtp.example.com -Port 587
```

#### Tester avec telnet

Activer le client Telnet via PowerShell (administrateur) :

```powershell
Enable-WindowsOptionalFeature -Online -FeatureName TelnetClient
```

Puis :

```cmd
telnet smtp.example.com 587
```

#### Tester avec OpenSSL sous Windows

Télécharger OpenSSL depuis https://slproweb.com/products/Win32OpenSSL.html, puis :

```cmd
openssl s_client -starttls smtp -connect smtp.example.com:587
```

#### Vérifier les enregistrements MX avec nslookup

```cmd
nslookup -type=MX example.com
```

#### Envoyer un email avec PowerShell

```powershell
$SmtpServer = "smtp.example.com"
$SmtpPort = 587
$Username = "expediteur@example.com"
$Password = ConvertTo-SecureString "motdepasse" -AsPlainText -Force
$Credential = New-Object System.Management.Automation.PSCredential ($Username, $Password)

Send-MailMessage -To "destinataire@example.com" -From "expediteur@example.com" -Subject "Test SMTP" -Body "Ceci est un test depuis PowerShell." -SmtpServer $SmtpServer -Port $SmtpPort -UseSsl -Credential $Credential
```

### 4.11. Envoi d'un email manuellement

#### Méthode avec telnet (port 25 ou 587)

```bash
telnet smtp.example.com 25
```

Interaction :

```
220 smtp.example.com ESMTP Postfix
EHLO monpc.example.com
250-smtp.example.com
250-PIPELINING
250-SIZE 52428800
250-STARTTLS
250-AUTH PLAIN LOGIN
250-ENHANCEDSTATUSCODES
250 8BITMIME
MAIL FROM:<moi@example.com>
250 2.1.0 Ok
RCPT TO:<ami@example.com>
250 2.1.5 Ok
DATA
354 End data with <CR><LF>.<CR><LF>
From: moi@example.com
To: ami@example.com
Subject: Salut
Date: Mon, 01 Jan 2026 12:00:00 +0000

Bonjour,

Ceci est un email envoyé manuellement via SMTP.

Cordialement,
Moi
.
250 2.0.0 Ok: queued as ABC123DEF
QUIT
221 2.0.0 Bye
```

#### Méthode avec Python

```python
import smtplib
from email.mime.text import MIMEText

msg = MIMEText("Bonjour, ceci est un test.")
msg['Subject'] = 'Test SMTP Python'
msg['From'] = 'expediteur@example.com'
msg['To'] = 'destinataire@example.com'

with smtplib.SMTP('smtp.example.com', 587) as server:
    server.starttls()
    server.login('expediteur@example.com', 'motdepasse')
    server.send_message(msg)
```

### 4.12. En-têtes SMTP

Les en-têtes email fournissent des métadonnées essentielles. Voici les principaux :

- `From` : Adresse de l'expéditeur affichée.
- `To` : Adresse du destinataire principal.
- `Cc` : Destinataires en copie.
- `Bcc` : Destinataires en copie cachée.
- `Subject` : Sujet du message.
- `Date` : Date et heure d'envoi.
- `Message-ID` : Identifiant unique du message.
- `In-Reply-To` : Identifiant du message auquel on répond.
- `References` : Liste des Message-ID liés.
- `Reply-To` : Adresse de réponse.
- `MIME-Version` : Version MIME utilisée.
- `Content-Type` : Type de contenu (text/plain, text/html, multipart/mixed, etc.).
- `Content-Transfer-Encoding` : Encodage du contenu (7bit, 8bit, base64, quoted-printable).
- `Received` : Trace du parcours du message à travers les serveurs.
- `Return-Path` : Adresse de retour en cas d'erreur.
- `X-Mailer` : Logiciel utilisé pour envoyer le message.

### 4.13. SPF, DKIM, DMARC

Ces mécanismes permettent d'authentifier les emails et de lutter contre le spam et le phishing.

#### SPF (Sender Policy Framework)

SPF permet au propriétaire d'un domaine de spécifier quels serveurs sont autorisés à envoyer des emails pour ce domaine. Il s'agit d'un enregistrement DNS de type TXT.

Exemple d'enregistrement SPF :

```
v=spf1 ip4:192.0.2.0/24 include:_spf.google.com ~all
```

- `v=spf1` : Version SPF.
- `ip4:` : Adresses IPv4 autorisées.
- `include:` : Inclure la politique d'un autre domaine.
- `~all` : Soft fail (les emails non conformes sont marqués mais pas forcément rejetés).
- `-all` : Hard fail (les emails non conformes sont rejetés).
- `+all` : Tous les serveurs sont autorisés (dangereux).
- `?all` : Neutre.

#### DKIM (DomainKeys Identified Mail)

DKIM ajoute une signature cryptographique aux emails, permettant de vérifier que le message n'a pas été altéré et qu'il provient bien d'un serveur autorisé. La clé publique est publiée dans un enregistrement DNS TXT.

Exemple d'enregistrement DKIM :

```
selector._domainkey.example.com. IN TXT "v=DKIM1; k=rsa; p=MIGfMA0GCSqGSIb3DQEBAQUAA4GNADCBiQKBgQC..."
```

#### DMARC (Domain-based Message Authentication, Reporting, and Conformance)

DMARC permet de définir une politique concernant l'utilisation de SPF et DKIM, et de recevoir des rapports sur les emails envoyés au nom du domaine.

Exemple d'enregistrement DMARC :

```
_dmarc.example.com. IN TXT "v=DMARC1; p=quarantine; rua=mailto:dmarc@example.com; pct=100; adkim=r; aspf=r"
```

- `p=none` : Aucune action, rapports uniquement.
- `p=quarantine` : Mettre en quarantaine les emails non conformes.
- `p=reject` : Rejeter les emails non conformes.
- `rua=` : Adresse de rapport agrégé.
- `ruf=` : Adresse de rapport forensic.

### 4.14. SMTP Auth et Relay

Le relay SMTP ouvert est un serveur qui accepte d'envoyer des emails pour n'importe qui, sans authentification. C'était courant dans les années 1990, mais c'est aujourd'hui une pratique dangereuse car elle permet l'envoi de spam.

L'authentification SMTP (SMTP AUTH) oblige les clients à s'identifier avant de pouvoir envoyer des emails. Les mécanismes d'authentification courants sont :

- `PLAIN` : Nom d'utilisateur et mot de passe en clair, à utiliser uniquement sur TLS.
- `LOGIN` : Similaire à PLAIN, mais avec un challenge en base64.
- `CRAM-MD5` : Authentification par défi/réponse, plus sécurisée.
- `XOAUTH2` : Utilisé par Gmail et Outlook pour l'authentification OAuth2.

### 4.15. Dépannage SMTP

#### Problème : impossible de se connecter au serveur SMTP

Vérifier la connectivité réseau :

```bash
ping smtp.example.com
telnet smtp.example.com 587
```

Vérifier le pare-feu :

```bash
sudo iptables -L -n | grep 587
sudo ufw status
```

#### Problème : erreur 550 (boîte aux lettres indisponible)

- Vérifier l'adresse du destinataire.
- Vérifier que le domaine existe et a un enregistrement MX valide.
- Vérifier que le serveur de destination n'a pas blacklisté l'expéditeur.

#### Problème : email marqué comme spam

- Vérifier la configuration SPF, DKIM et DMARC.
- Vérifier la réputation de l'adresse IP.
- Vérifier le contenu du message.
- Consulter les blacklists (RBL) comme Spamhaus, Barracuda, SURBL.

---

## POP3 - Post Office Protocol v3

### 5.1. Définition et rôle

POP3 est un protocole utilisé pour récupérer des emails depuis un serveur de messagerie vers un client local. Conçu à l'origine pour les connexions intermittentes, POP3 télécharge généralement les messages sur un seul appareil et les supprime du serveur (selon la configuration).

POP3 est simple, léger et rapide, mais il offre des fonctionnalités limitées par rapport à IMAP. Il ne permet pas de gérer facilement plusieurs dossiers, ni de synchroniser l'état de lecture entre plusieurs appareils.

### 5.2. Historique

- 1984 : POP1 défini dans la RFC 918.
- 1985 : POP2 défini dans la RFC 937.
- 1988 : POP3 introduit dans la RFC 1081.
- 1996 : POP3 standardisé dans la RFC 1939.
- 1999 : Extension POP3 pour TLS dans la RFC 2595.
- 2003 : Extension SASL dans la RFC 5034.
- 2018 : RFC 8314 encourage l'utilisation de TLS implicite sur le port 995.

### 5.3. Architecture POP3

L'architecture POP3 est client-serveur :

- **Serveur POP3** : Héberge les boîtes aux lettres et attend les connexions des clients.
- **Client POP3** : Se connecte au serveur, s'authentifie, récupère les messages et éventuellement les supprime.

Les messages sont stockés sur le serveur jusqu'à ce que le client les télécharge. Selon la configuration, les messages peuvent être conservés ou supprimés du serveur après téléchargement.

### 5.4. Fonctionnement détaillé

Une session POP3 typique suit les étapes suivantes :

1. Le client établit une connexion TCP sur le port 110 (non sécurisé) ou 995 (POP3S).
2. Le serveur envoie un message de bienvenue.
3. Le client envoie `USER` suivi du nom d'utilisateur.
4. Le client envoie `PASS` suivi du mot de passe.
5. Le serveur ouvre la boîte aux lettres et indique le nombre de messages.
6. Le client peut lister les messages (`LIST`), les récupérer (`RETR`), les supprimer (`DELE`), etc.
7. Le client termine avec `QUIT`, ce qui valide les suppressions.

### 5.5. Commandes POP3

- `USER nom_utilisateur` : Envoie le nom d'utilisateur.
- `PASS mot_de_passe` : Envoie le mot de passe.
- `STAT` : Retourne le nombre de messages et leur taille totale.
- `LIST [msg]` : Liste les messages et leurs tailles.
- `RETR msg` : Récupère le message spécifié.
- `DELE msg` : Marque le message pour suppression.
- `NOOP` : Aucune opération.
- `RSET` : Réinitialise les marques de suppression.
- `QUIT` : Termine la session et supprime les messages marqués.
- `TOP msg n` : Récupère les n premières lignes du message.
- `UIDL [msg]` : Retourne l'identifiant unique du message.
- `CAPA` : Liste les capacités du serveur (extension).
- `STLS` : Passe en TLS (extension).
- `AUTH` : Authentification SASL (extension).

### 5.6. États de session POP3

Une session POP3 comporte trois états :

1. **AUTHORIZATION** : L'utilisateur doit s'authentifier avec `USER` et `PASS`.
2. **TRANSACTION** : L'utilisateur peut consulter, récupérer et marquer les messages.
3. **UPDATE** : Après `QUIT`, les messages marqués sont supprimés et la session se termine.

### 5.7. Ports et sécurité

- **Port 110** : POP3 non chiffré. Déconseillé aujourd'hui.
- **Port 995** : POP3S, avec TLS implicite. Recommandé.
- **STARTTLS sur le port 110** : Permet de passer en TLS après la connexion (extension `STLS`).

Il est fortement recommandé d'utiliser le port 995 avec TLS pour protéger les identifiants et le contenu des emails.

### 5.8. Configuration POP3

#### Configuration d'un client POP3

- **Serveur POP3** : `pop.example.com`
- **Port** : `995` (SSL/TLS) ou `110` (non sécurisé)
- **Méthode de chiffrement** : SSL/TLS ou STARTTLS
- **Nom d'utilisateur** : L'adresse email complète
- **Mot de passe** : Le mot de passe du compte
- **Conserver une copie sur le serveur** : Option souvent disponible dans le client

#### Configuration de Dovecot pour POP3

Dovecot est un serveur POP3/IMAP très populaire. Exemple de configuration dans `/etc/dovecot/dovecot.conf` :

```ini
protocols = imap pop3 lmtp
listen = *, ::

ssl = required
ssl_cert = </etc/dovecot/dovecot.pem
ssl_key = </etc/dovecot/private/dovecot.pem

passdb {
  driver = passwd-file
  args = /etc/dovecot/users
}

userdb {
  driver = static
  args = uid=vmail gid=vmail home=/var/mail/%d/%n
}

protocol pop3 {
  pop3_uidl_format = %08Xu%08Xv
}
```

### 5.9. Vérification et tests sous Linux

#### Vérifier que le service POP3 écoute

```bash
sudo ss -tlnp | grep -E ':110|:995'
```

#### Tester POP3 avec telnet

```bash
telnet pop.example.com 110
```

Interaction :

```
+OK Dovecot ready.
USER alice@example.com
+OK
PASS secret
+OK Logged in.
STAT
+OK 3 4520
LIST
+OK 3 messages (4520 octets)
1 1500
2 2000
3 1020
.
RETR 1
+OK 1500 octets
[contenu du message]
.
DELE 1
+OK Marked to be deleted.
QUIT
+OK Logging out.
```

#### Tester POP3S avec OpenSSL

```bash
openssl s_client -connect pop.example.com:995
```

#### Utiliser `fetchmail` pour récupérer des emails

Configuration dans `~/.fetchmailrc` :

```ini
poll pop.example.com
  protocol pop3
  username "alice@example.com" password "secret"
  ssl
  keep
  mda "/usr/bin/procmail"
```

Exécution :

```bash
fetchmail -v
```

### 5.10. Vérification et tests sous Windows

#### Tester avec Telnet

```cmd
telnet pop.example.com 110
```

#### Tester avec OpenSSL

```cmd
openssl s_client -connect pop.example.com:995
```

#### Configurer Windows Mail / Outlook pour POP3

1. Ouvrir Outlook.
2. Aller dans Fichier > Ajouter un compte.
3. Choisir Configuration manuelle.
4. Sélectionner POP ou IMAP.
5. Renseigner :
   - Serveur entrant : `pop.example.com`, port 995, SSL/TLS
   - Serveur sortant : `smtp.example.com`, port 587, STARTTLS
   - Nom d'utilisateur et mot de passe

### 5.11. Récupération manuelle d'emails

#### Session POP3S complète avec OpenSSL

```bash
openssl s_client -connect pop.gmail.com:995 -crlf
```

Interaction :

```
+OK Gpop ready for requests from 203.0.113.1 a1mb1234567890edc
USER alice@gmail.com
+OK send PASS
PASS application_password
+OK Welcome.
STAT
+OK 10 52400
LIST
+OK 10 messages
1 3200
2 4500
...
.
RETR 1
+OK 3200 octets
Return-Path: <bob@example.com>
...
.
QUIT
+OK Farewell.
```

### 5.12. Dépannage POP3

#### Problème : connexion refusée

- Vérifier que le serveur POP3 est actif.
- Vérifier le pare-feu.
- Vérifier le port utilisé (110 ou 995).

#### Problème : authentification échouée

- Vérifier le nom d'utilisateur et le mot de passe.
- Vérifier si un mot de passe d'application est nécessaire (Gmail, Outlook).
- Vérifier les logs du serveur Dovecot ou du serveur de messagerie.

#### Problème : les emails disparaissent du serveur

- Vérifier si l'option "Supprimer les messages du serveur après téléchargement" est activée.
- Utiliser `keep` avec fetchmail pour conserver les messages.

---

## IMAP - Internet Message Access Protocol

### 6.1. Définition et rôle

IMAP est un protocole sophistiqué permettant aux clients de messagerie d'accéder à leurs emails directement sur le serveur. Contrairement à POP3, IMAP conserve les messages sur le serveur et permet de gérer des dossiers, des drapeaux (lus, répondu, important, etc.) et de synchroniser l'état entre plusieurs appareils.

IMAP est particulièrement adapté aux utilisateurs modernes qui consultent leurs emails depuis plusieurs appareils (ordinateur, smartphone, tablette, webmail).

### 6.2. Historique

- 1986 : Mark Crispin commence le développement d'IMAP au Stanford Knowledge Systems Laboratory.
- 1988 : RFC 1064, première spécification expérimentale.
- 1990 : RFC 1176, IMAP version 2.
- 1994 : RFC 1730, IMAP4.
- 1996 : RFC 2060, révision d'IMAP4rev1.
- 2003 : RFC 3501, IMAP4rev1 standardisé.
- 2021 : RFC 9051, IMAP4rev2 avec de nouvelles fonctionnalités.

### 6.3. Architecture IMAP

L'architecture IMAP est également client-serveur :

- **Serveur IMAP** : Stocke les messages dans une hiérarchie de dossiers (boîtes aux lettres) et répond aux commandes des clients.
- **Client IMAP** : Se connecte, s'authentifie, puis manipule les messages directement sur le serveur.

IMAP permet de gérer des boîtes aux lettres nommées, de rechercher des messages, de définir des drapeaux, et de télécharger uniquement certaines parties d'un message (par exemple, l'en-tête uniquement).

### 6.4. Fonctionnement détaillé

Une session IMAP typique suit les étapes suivantes :

1. Le client établit une connexion TCP sur le port 143 (non chiffré) ou 993 (IMAPS).
2. Le serveur envoie un message de bienvenue.
3. Le client s'authentifie avec `LOGIN` ou une méthode SASL.
4. Le client sélectionne une boîte aux lettres avec `SELECT`.
5. Le client récupère les informations des messages avec `FETCH`.
6. Le client peut définir des drapeaux (`STORE`), rechercher (`SEARCH`), copier (`COPY`), etc.
7. Le client ferme la session avec `LOGOUT`.

### 6.5. Commandes IMAP

- `CAPABILITY` : Liste les capacités du serveur.
- `NOOP` : Aucune opération.
- `LOGOUT` : Termine la session.
- `LOGIN username password` : Authentification simple.
- `AUTHENTICATE mechanism` : Authentification SASL.
- `SELECT mailbox` : Sélectionne une boîte aux lettres en mode lecture/écriture.
- `EXAMINE mailbox` : Sélectionne une boîte en lecture seule.
- `CREATE mailbox` : Crée une boîte aux lettres.
- `DELETE mailbox` : Supprime une boîte aux lettres.
- `RENAME old new` : Renomme une boîte.
- `LIST reference pattern` : Liste les boîtes aux lettres.
- `LSUB reference pattern` : Liste les boîtes aux lettres abonnées.
- `STATUS mailbox items` : Retourne l'état d'une boîte sans la sélectionner.
- `APPEND mailbox message` : Ajoute un message à une boîte.
- `FETCH set items` : Récupère des données sur les messages.
- `STORE set item value` : Modifie les drapeaux ou les métadonnées.
- `COPY set mailbox` : Copie des messages vers une autre boîte.
- `UID command` : Exécute une commande avec des UID.
- `SEARCH criteria` : Recherche des messages.
- `SORT` : Trie les résultats d'une recherche.
- `THREAD` : Renvoie les conversations sous forme d'arborescence.
- `STARTTLS` : Passe la connexion en TLS.
- `IDLE` : Permet au serveur d'informer le client des nouveaux messages.

### 6.6. États de session IMAP

Une session IMAP comporte quatre états :

1. **Not Authenticated** : Le client doit s'authentifier.
2. **Authenticated** : Le client est authentifié mais n'a pas sélectionné de boîte.
3. **Selected** : Le client a sélectionné une boîte aux lettres.
4. **Logout** : La session se termine.

### 6.7. Ports et sécurité

- **Port 143** : IMAP non chiffré. Déconseillé.
- **Port 993** : IMAPS, avec TLS implicite. Recommandé.
- **STARTTLS sur le port 143** : Passe en TLS après la connexion.

IMAP supporte également des mécanismes d'authentification robustes comme SCRAM-SHA-256, et des extensions de sécurité comme SASL-IR, ID, et CONDSTORE.

### 6.8. Configuration IMAP

#### Configuration d'un client IMAP

- **Serveur IMAP** : `imap.example.com`
- **Port** : `993` (SSL/TLS)
- **Méthode de chiffrement** : SSL/TLS
- **Nom d'utilisateur** : L'adresse email complète
- **Mot de passe** : Le mot de passe du compte

#### Configuration de Dovecot pour IMAP

Exemple de configuration dans `/etc/dovecot/conf.d/10-mail.conf` :

```ini
mail_location = maildir:~/Maildir
namespace inbox {
  inbox = yes
}
```

Dans `/etc/dovecot/conf.d/10-auth.conf` :

```ini
disable_plaintext_auth = yes
auth_mechanisms = plain login scram-sha-256
```

Dans `/etc/dovecot/conf.d/10-ssl.conf` :

```ini
ssl = required
ssl_cert = </etc/dovecot/dovecot.pem
ssl_key = </etc/dovecot/private/dovecot.pem
ssl_min_protocol = TLSv1.2
```

### 6.9. Vérification et tests sous Linux

#### Vérifier que le service IMAP écoute

```bash
sudo ss -tlnp | grep -E ':143|:993'
```

#### Tester IMAP avec OpenSSL

```bash
openssl s_client -connect imap.example.com:993 -crlf
```

Interaction :

```
* OK [CAPABILITY IMAP4rev1 ...] Dovecot ready.
a1 LOGIN alice@example.com secret
a1 OK [CAPABILITY ...] Logged in
a2 LIST "" "*"
* LIST (\HasNoChildren) "." INBOX
* LIST (\HasNoChildren) "." Sent
a2 OK List completed.
a3 SELECT INBOX
* FLAGS (\Answered \Flagged \Deleted \Seen \Draft)
* OK [PERMANENTFLAGS (\Answered \Flagged \Deleted \Seen \Draft \*)] Flags permitted.
* 5 EXISTS
* 0 RECENT
a3 OK [READ-WRITE] Select completed.
a4 FETCH 1:5 (FLAGS BODY[HEADER.FIELDS (SUBJECT FROM DATE)])
* 1 FETCH (FLAGS (\Seen) BODY[HEADER.FIELDS (SUBJECT FROM DATE)] {120}
...
)
a4 OK Fetch completed.
a5 LOGOUT
* BYE Logging out
a5 OK Logout completed.
```

#### Utiliser `imapsync`

`imapsync` permet de migrer des emails entre deux serveurs IMAP :

```bash
imapsync --host1 imap.source.com --user1 alice --password1 "secret1" \
         --host2 imap.dest.com --user2 alice --password2 "secret2" \
         --ssl1 --ssl2
```

#### Utiliser `mutt` en mode IMAP

```bash
mutt -f imaps://alice@example.com@imap.example.com
```

### 6.10. Vérification et tests sous Windows

#### Tester avec OpenSSL

```cmd
openssl s_client -connect imap.example.com:993 -crlf
```

#### Configurer Outlook pour IMAP

1. Ouvrir Outlook.
2. Fichier > Ajouter un compte.
3. Choisir Configuration manuelle.
4. Sélectionner POP ou IMAP.
5. Renseigner :
   - Serveur entrant : `imap.example.com`, port 993, SSL/TLS
   - Serveur sortant : `smtp.example.com`, port 587, STARTTLS
   - Nom d'utilisateur et mot de passe

### 6.11. Manipulation manuelle de boîtes IMAP

#### Créer un dossier

```
a1 LOGIN alice@example.com secret
a2 CREATE Archives.2026
a2 OK Create completed.
```

#### Rechercher des messages non lus

```
a1 LOGIN alice@example.com secret
a2 SELECT INBOX
a3 SEARCH UNSEEN
* SEARCH 2 5 8
a3 OK Search completed.
```

#### Marquer un message comme lu

```
a4 STORE 2 FLAGS (\Seen)
* 2 FETCH (FLAGS (\Seen))
a4 OK Store completed.
```

#### Copier un message vers un autre dossier

```
a5 COPY 2 Archives.2026
a5 OK Copy completed.
```

### 6.12. Dépannage IMAP

#### Problème : connexion refusée ou timeout

- Vérifier que le serveur IMAP écoute sur le bon port.
- Vérifier le pare-feu et les règles réseau.
- Vérifier les certificats SSL/TLS.

#### Problème : authentification échouée

- Vérifier les identifiants.
- Vérifier que `disable_plaintext_auth` n'est pas activé sans TLS.
- Consulter les logs Dovecot (`/var/log/mail.log`).

#### Problème : synchronisation lente

- Vérifier la taille des boîtes aux lettres.
- Activer la compression IMAP (`COMPRESS=DEFLATE`).
- Utiliser IDLE pour les notifications push.

---

## Comparatif SMTP / POP3 / IMAP

| Critère | SMTP | POP3 | IMAP |
|---------|------|------|------|
| Rôle | Envoi de emails | Réception/téléchargement | Accès et gestion sur serveur |
| Port standard | 25, 587, 465 | 110, 995 | 143, 993 |
| Chiffrement recommandé | STARTTLS/SSL-TLS | SSL/TLS (port 995) | SSL/TLS (port 993) |
| Stockage des messages | Transitoire | Local (par défaut) | Sur le serveur |
| Multi-appareils | Non applicable | Limité | Excellent |
| Gestion des dossiers | Non | Limitée | Complète |
| Synchronisation d'état | Non | Non | Oui |
| Bande passante | Faible | Téléchargement complet | Optimisée |
| Complexité | Moyenne | Faible | Élevée |
| Utilisation typique | Relai d'envoi | Client unique, connexion lente | Clients multiples, productivité |

---

## Où et comment sont utilisés ces protocoles

### SMTP

SMTP est utilisé partout où des emails sont envoyés :

- **Webmails** : Gmail, Outlook.com, Yahoo Mail, ProtonMail envoient tous via SMTP.
- **Clients de messagerie** : Thunderbird, Outlook, Apple Mail utilisent SMTP pour l'envoi.
- **Applications et sites web** : Les formulaires de contact, les notifications, les newsletters utilisent SMTP.
- **Serveurs d'entreprise** : Microsoft Exchange, Postfix, Sendmail, Exim relaient les emails internes et externes.
- **Objets connectés** : Certains systèmes embarqués envoient des alertes par SMTP.
- **Scripts et automatisations** : Les systèmes de surveillance envoient des alertes email.

### POP3

POP3 est utilisé dans des contextes spécifiques :

- **Connexons lentes ou intermittentes** : Téléchargement complet pour consultation hors ligne.
- **Sauvegarde locale** : Archivage des emails sur un ordinateur.
- **Clients légères** : Certains clients mobiles anciens ou systèmes embarqués.
- **Confidentialité** : Certains utilisateurs préfèrent ne pas laisser leurs messages sur le serveur.

### IMAP

IMAP est le protocole dominant pour la consultation moderne :

- **Messagerie multi-appareils** : Synchronisation entre ordinateur, smartphone et tablette.
- **Webmails** : La plupart des webmails utilisent IMAP en arrière-plan.
- **Collaboration** : Dossiers partagés, brouillons synchronisés.
- **Recherche avancée** : Indexation et recherche côté serveur.
- **Gestion centralisée** : Sauvegardes, quotas et politiques de rétention côté serveur.

---

## Applications et logiciels utilisant ces protocoles

### Clients de messagerie

- **Mozilla Thunderbird** : Client libre et multiplateforme supportant SMTP, POP3 et IMAP.
- **Microsoft Outlook** : Client professionnel très répandu.
- **Apple Mail** : Client natif macOS et iOS.
- **Evolution** : Client de messagerie pour Linux (GNOME).
- **KMail** : Client de messagerie pour Linux (KDE).
- **Geary** : Client léger pour Linux.
- **Mailspring** : Client moderne et rapide.
- **eM Client** : Client pour Windows et macOS.
- **Mailbird** : Client pour Windows.
- **FairEmail** : Client sécurisé pour Android.

### Serveurs de messagerie

- **Postfix** : MTA moderne, sécurisé et populaire.
- **Sendmail** : MTA historique très puissant.
- **Exim** : MTA flexible et largement utilisé.
- **Microsoft Exchange** : Solution complète pour les entreprises.
- **Dovecot** : Serveur POP3/IMAP open source.
- **Courier** : Suite serveur de messagerie.
- **Cyrus IMAP** : Serveur IMAP robuste pour les grandes organisations.
- **Zimbra** : Plateforme de collaboration open source.
- **Mailcow** : Suite de messagerie complète basée sur Docker.
- **iRedMail** : Solution de messagerie facile à déployer.

### Outils de test et d'administration

- **swaks** : Testeur SMTP avancé.
- **OpenSSL** : Tests SSL/TLS pour POP3S/IMAPS/SMTPS.
- **Telnet** : Tests manuels de protocoles.
- **Netcat (nc)** : Tests réseau.
- **dig / nslookup** : Requêtes DNS (MX, TXT).
- **fetchmail** : Récupération POP3/IMAP.
- **getmail** : Alternative à fetchmail.
- **imapsync** : Migration IMAP.
- **mb2md** : Conversion mbox vers Maildir.
- **procmail** : Filtrage et livraison d'emails.
- **mailq / postqueue** : Gestion des files d'attente Postfix.
- **mutt** : Client en ligne de commande.
- **alpine** : Client email en ligne de commande.

---

## Configuration sur les principaux serveurs

### Configuration de Postfix

Fichier `/etc/postfix/main.cf` :

```ini
# Nom d'hôte et domaine
myhostname = mail.example.com
mydomain = example.com
myorigin = $mydomain
inet_interfaces = all
mydestination = $myhostname, localhost.$mydomain, localhost, $mydomain
mynetworks = 127.0.0.0/8 [::ffff:127.0.0.0]/104 [::1]/128

# Stockage
home_mailbox = Maildir/
mailbox_size_limit = 0
recipient_delimiter = +

# TLS
smtpd_tls_cert_file = /etc/letsencrypt/live/example.com/fullchain.pem
smtpd_tls_key_file = /etc/letsencrypt/live/example.com/privkey.pem
smtpd_tls_security_level = may
smtp_tls_security_level = may
smtpd_tls_protocols = !SSLv2, !SSLv3
smtpd_tls_mandatory_protocols = !SSLv2, !SSLv3

# Authentification SASL
smtpd_sasl_type = dovecot
smtpd_sasl_path = private/auth
smtpd_sasl_auth_enable = yes
smtpd_sasl_security_options = noanonymous
smtpd_sasl_local_domain = $myhostname
broken_sasl_auth_clients = yes

# Restrictions
smtpd_helo_required = yes
smtpd_recipient_restrictions =
    permit_mynetworks,
    permit_sasl_authenticated,
    reject_unauth_destination,
    reject_invalid_hostname,
    reject_non_fqdn_hostname,
    reject_non_fqdn_sender,
    reject_non_fqdn_recipient,
    reject_unknown_sender_domain,
    reject_unknown_recipient_domain,
    reject_rbl_client zen.spamhaus.org

# Limites
message_size_limit = 52428800
smtpd_hard_error_limit = 10
```

### Configuration de Dovecot

Fichier `/etc/dovecot/dovecot.conf` :

```ini
protocols = imap pop3 lmtp
listen = *, ::

# Authentification
passdb {
  driver = passwd-file
  args = /etc/dovecot/users
}

userdb {
  driver = static
  args = uid=vmail gid=vmail home=/var/mail/%d/%n
}

# SSL
ssl = required
ssl_cert = </etc/letsencrypt/live/example.com/fullchain.pem
ssl_key = </etc/letsencrypt/live/example.com/privkey.pem
ssl_min_protocol = TLSv1.2

# IMAP
protocol imap {
  mail_max_userip_connections = 30
}

# POP3
protocol pop3 {
  pop3_uidl_format = %08Xu%08Xv
}

# LMTP pour Postfix
protocol lmtp {
  postmaster_address = postmaster@example.com
  mail_plugins = $mail_plugins sieve
}
```

### Configuration d'Exim

Fichier `/etc/exim/exim.conf` (exemple simplifié) :

```ini
primary_hostname = mail.example.com
domainlist local_domains = @ : example.com
domainlist relay_to_domains =
hostlist relay_from_hosts = 127.0.0.1

acl_check_rcpt:
  accept hosts = :
  accept authenticated = *
  accept domains = +local_domains
  deny message = relay not permitted

begin routers
localuser:
  driver = accept
  domains = +local_domains
  local_parts = postmaster : abuse
  transport = local_delivery
  route_data = ${local_part}

begin transports
local_delivery:
  driver = appendfile
  directory = /var/mail/$local_part
  delivery_date_add
  envelope_to_add
  return_path_add
```

### Configuration de Microsoft Exchange

Microsoft Exchange utilise des interfaces graphiques et PowerShell. Exemple de configuration d'un connecteur d'envoi :

```powershell
New-SendConnector -Name "Internet Connector" -AddressSpaces "*" -DNSRoutingEnabled $true -Usage "Internet"
```

Configuration d'un connecteur de réception pour la soumission authentifiée :

```powershell
New-ReceiveConnector -Name "Client Submission" -Usage Client -Bindings 0.0.0.0:587 -AuthMechanism Tls,BasicAuth,BasicAuthRequireTLS
```

---

## Sécurité de la messagerie

### Menaces courantes

- **Spam** : Envoi massif non sollicité.
- **Phishing** : Emails frauduleux visant à voler des informations.
- **Malware** : Pièces jointes infectées.
- **Spoofing** : Falsification de l'adresse de l'expéditeur.
- **Man-in-the-middle** : Interception des communications.
- **Déni de service** : Saturation des serveurs de messagerie.
- **Fuites de données** : Exfiltration via la messagerie.

### Bonnes pratiques

- Toujours utiliser TLS pour SMTP, POP3 et IMAP.
- Désactiver les protocoles non chiffrés (ports 25/110/143 pour les clients).
- Mettre en place SPF, DKIM et DMARC.
- Utiliser des mots de passe forts et de l'authentification multi-facteurs.
- Limiter le relai SMTP aux utilisateurs authentifiés.
- Surveiller les logs et les files d'attente.
- Maintenir les serveurs à jour.
- Utiliser des listes noires (RBL) et des filtres anti-spam.
- Segmenter le réseau et restreindre l'accès aux serveurs de messagerie.
- Sauvegarder régulièrement les boîtes aux lettres.

### MTA-STS

MTA-STS (Mail Transfer Agent Strict Transport Security) permet de forcer l'utilisation de TLS pour les échanges inter-serveurs SMTP. Il repose sur un fichier publié en HTTPS et un enregistrement DNS TXT `_mta-sts`.

Exemple d'enregistrement DNS :

```
_mta-sts.example.com. IN TXT "v=STSv1; id=20260101T000000;"
```

Fichier `https://mta-sts.example.com/.well-known/mta-sts.txt` :

```
version: STSv1
mode: enforce
max_age: 604800
mx: mail.example.com
mx: mail2.example.com
```

### TLS Reporting

TLS-RPT permet de recevoir des rapports sur les échecs de validation TLS. Enregistrement DNS :

```
_smtp._tls.example.com. IN TXT "v=TLSRPTv1; rua=mailto:tls-rpt@example.com"
```

---

## Commandes de vérification réseau

### Linux

#### Vérifier la résolution DNS

```bash
nslookup example.com
dig example.com MX
host -t MX example.com
```

#### Vérifier la connectivité TCP

```bash
telnet smtp.example.com 587
nc -vz smtp.example.com 587
nc -vz imap.example.com 993
nc -vz pop.example.com 995
```

#### Vérifier les certificats TLS

```bash
openssl s_client -connect smtp.example.com:465 -servername example.com
openssl s_client -connect imap.example.com:993 -servername example.com
openssl s_client -connect pop.example.com:995 -servername example.com
```

#### Vérifier la chaîne SPF/DKIM/DMARC

```bash
dig TXT _spf.example.com
dig TXT default._domainkey.example.com
dig TXT _dmarc.example.com
```

#### Scanner les ports

```bash
nmap -p 25,110,143,465,587,993,995 mail.example.com
```

#### Suivre le routage

```bash
traceroute mail.example.com
mtr mail.example.com
```

### Windows

#### Vérifier la résolution DNS

```cmd
nslookup example.com
nslookup -type=MX example.com
```

#### Vérifier la connectivité TCP

```powershell
Test-NetConnection -ComputerName smtp.example.com -Port 587
Test-NetConnection -ComputerName imap.example.com -Port 993
Test-NetConnection -ComputerName pop.example.com -Port 995
```

#### Vérifier les certificats TLS

```cmd
openssl s_client -connect smtp.example.com:465 -servername example.com
```

#### Scanner les ports

```powershell
Test-NetConnection -ComputerName mail.example.com -Port 25
Test-NetConnection -ComputerName mail.example.com -Port 110
Test-NetConnection -ComputerName mail.example.com -Port 143
Test-NetConnection -ComputerName mail.example.com -Port 465
Test-NetConnection -ComputerName mail.example.com -Port 587
Test-NetConnection -ComputerName mail.example.com -Port 993
Test-NetConnection -ComputerName mail.example.com -Port 995
```

#### Suivre le routage

```cmd
tracert mail.example.com
```

---

## Exercices pratiques

### Exercice 1 : Envoyer un email avec telnet

Objectif : Envoyer un email manuellement via SMTP sur le port 587.

Étapes :
1. Identifier le serveur SMTP et le port.
2. Établir une connexion avec telnet ou OpenSSL.
3. Envoyer les commandes EHLO, MAIL FROM, RCPT TO, DATA.
4. Rédiger un message avec sujet et corps.
5. Terminer avec `.` puis `QUIT`.

### Exercice 2 : Vérifier les enregistrements MX

Objectif : Trouver les serveurs de messagerie d'un domaine.

```bash
dig MX gmail.com
```

### Exercice 3 : Configurer Thunderbird

Objectif : Configurer un compte email avec IMAP et SMTP.

1. Ouvrir Thunderbird.
2. Ajouter un compte existant.
3. Renseigner l'adresse email et le mot de passe.
4. Vérifier les paramètres IMAP (port 993, SSL/TLS) et SMTP (port 587, STARTTLS).
5. Tester l'envoi et la réception.

### Exercice 4 : Récupérer un email avec POP3

Objectif : Se connecter à un serveur POP3S et récupérer un message.

```bash
openssl s_client -connect pop.example.com:995
```

Utiliser `USER`, `PASS`, `LIST`, `RETR` et `QUIT`.

### Exercice 5 : Naviguer dans une boîte IMAP

Objectif : Lister les dossiers, sélectionner la boîte de réception et rechercher les messages non lus.

```bash
openssl s_client -connect imap.example.com:993 -crlf
```

Utiliser `LOGIN`, `LIST`, `SELECT`, `SEARCH UNSEEN`, `FETCH`, `STORE` et `LOGOUT`.

### Exercice 6 : Configurer SPF, DKIM et DMARC

Objectif : Sécuriser un domaine contre le spoofing.

1. Créer un enregistrement SPF.
2. Générer une paire de clés DKIM avec opendkim-genkey.
3. Publier la clé publique dans le DNS.
4. Créer un enregistrement DMARC.
5. Vérifier avec des outils en ligne.

### Exercice 7 : Analyser les en-têtes d'un email

Objectif : Comprendre le parcours d'un email.

1. Afficher les en-têtes complets d'un email reçu.
2. Identifier les champs `Received`.
3. Vérifier les signatures DKIM-Signature.
4. Rechercher les champs Authentication-Results.

---

## Ressources, livres et liens

### RFCs essentielles

- RFC 821 - Simple Mail Transfer Protocol (1982)
- RFC 822 - Standard for the Format of ARPA Internet Text Messages (1982)
- RFC 937 - Post Office Protocol - Version 2 (1985)
- RFC 1939 - Post Office Protocol - Version 3 (1996)
- RFC 2595 - Using TLS with IMAP, POP3 and ACAP (1999)
- RFC 2821 - Simple Mail Transfer Protocol (2001, obsolète)
- RFC 3207 - SMTP Service Extension for Secure SMTP over TLS (2002)
- RFC 3501 - Internet Message Access Protocol - Version 4rev1 (2003)
- RFC 4409 - Message Submission for Mail (2006)
- RFC 4954 - SMTP Service Extension for Authentication (2007)
- RFC 5321 - Simple Mail Transfer Protocol (2008)
- RFC 5322 - Internet Message Format (2008)
- RFC 6409 - Message Submission for Mail (2011)
- RFC 7208 - Sender Policy Framework (2014)
- RFC 6376 - DomainKeys Identified Mail (DKIM) Signatures (2011)
- RFC 7489 - Domain-based Message Authentication, Reporting, and Conformance (DMARC) (2015)
- RFC 7817 - TLS Session Ticket Extension for IMAP (2016)
- RFC 8314 - Cleartext Considered Obsolete: Use of TLS for Email Submission and Access (2018)
- RFC 8461 - SMTP MTA Strict Transport Security (MTA-STS) (2018)
- RFC 8460 - SMTP TLS Reporting (2018)
- RFC 9051 - Internet Message Access Protocol - Version 4rev2 (2021)

### Livres recommandés

- "Postfix: The Definitive Guide" par Kyle D. Dent
- "The Book of Postfix" par Ralf Hildebrandt et Patrick Koetter
- "Dovecot: POP3/IMAP Servers for Enterprises and ISPs" par Peer Heinlein
- "Email Security with Cisco IronPort" par Chris Porter
- "The Anti-Spam Toolkit" par Paul Wolfe
- "Building Internet Firewalls" par Elizabeth D. Zwicky, Simon Cooper et D. Brent Chapman
- "DNS and BIND" par Cricket Liu et Paul Albitz
- "TCP/IP Illustrated" par W. Richard Stevens
- "Computer Networking: A Top-Down Approach" par James F. Kurose et Keith W. Ross
- "Hacking Exposed: Network Security Secrets & Solutions" par Stuart McClure, Joel Scambray et George Kurtz

### Liens utiles

- https://www.postfix.org/documentation.html
- https://doc.dovecot.org/
- https://www.exim.org/docs.html
- https://datatracker.ietf.org/
- https://mxtoolbox.com/
- https://www.mail-tester.com/
- https://dkimvalidator.com/
- https://dmarcian.com/
- https://support.google.com/mail/answer/7126229
- https://support.microsoft.com/fr-fr/office/paramètres-pop-imap-et-smtp-de-outlook-com-d088b986-291d-42b8-9564-9c414e2aa040
- https://www.spamhaus.org/
- https://www.barracuda.com/
- https://www.proofpoint.com/
- https://www.openssl.org/docs/
- https://www.cisco.com/c/en/us/products/security/email-security/index.html

### Applications mobiles

- Gmail (Android/iOS)
- Outlook (Android/iOS)
- Apple Mail (iOS)
- FairEmail (Android)
- Blue Mail (Android/iOS)
- Aqua Mail (Android)
- Nine (Android)
- Spark (Android/iOS)
- Edison Mail (Android/iOS)
- ProtonMail (Android/iOS)

### Outils en ligne

- MXToolbox : diagnostic DNS et messagerie
- Mail-Tester : évaluation de la délivrabilité
- DKIMValidator : validation DKIM
- DMARC Analyzer : analyse DMARC
- Google Admin Toolbox : diagnostics réseau
- Message Header Analyzer (Microsoft)
- Mailhardener : monitoring de sécurité email
- EasyDMARC : plateforme DMARC
- Valimail : authentification email
- Red Sift OnDMARC : analyse DMARC

---

## Glossaire

- **Bcc (Blind Carbon Copy)** : Copie cachée.
- **Cc (Carbon Copy)** : Copie.
- **DKIM** : Signature cryptographique d'email.
- **DMARC** : Politique d'authentification et de conformité.
- **DNS** : Système de noms de domaine.
- **ESMTP** : SMTP étendu.
- **IMAP** : Protocole d'accès aux messages Internet.
- **MUA** : Agent utilisateur de messagerie.
- **MTA** : Agent de transfert de messages.
- **MDA** : Agent de livraison de messages.
- **MIME** : Multipurpose Internet Mail Extensions.
- **MX** : Mail Exchanger (enregistrement DNS).
- **POP3** : Protocole de bureau de poste version 3.
- **RBL** : Real-time Blackhole List.
- **SASL** : Simple Authentication and Security Layer.
- **SMTP** : Simple Mail Transfer Protocol.
- **SPF** : Sender Policy Framework.
- **STARTTLS** : Commande pour passer en TLS.
- **TLS** : Transport Layer Security.
- **TLSA** : Enregistrement DNS pour DANE.
- **UID** : Identifiant unique d'un message IMAP.
- **UIDL** : Liste des identifiants uniques POP3.

---

## Conclusion

Les protocoles SMTP, POP3 et IMAP constituent les fondations de la messagerie électronique moderne. SMTP assure le transport des messages, POP3 permet le téléchargement local, et IMAP offre un accès avancé et synchronisé aux boîtes aux lettres sur le serveur.

La maîtrise de ces protocoles est essentielle pour les administrateurs système, les ingénieurs réseau et les professionnels de la cybersécurité. Avec l'évolution des menaces, il est crucial de mettre en œuvre les bonnes pratiques de sécurité : chiffrement TLS, authentification forte, SPF, DKIM, DMARC, MTA-STS et surveillance continue.

Ce document, rédigé par **hackers_tchad** en 2026, constitue une référence avancée pour comprendre, configurer, tester et sécuriser les protocoles de messagerie électronique. Il couvre les aspects théoriques, pratiques et opérationnels, avec des commandes pour Linux et Windows, des exemples de configuration, des exercices et de nombreuses ressources complémentaires.

Nous encourageons le lecteur à expérimenter dans un environnement de test, à consulter les RFCs officielles et à rester informé des évolutions des standards et des menaces. La messagerie reste un vecteur critique de communication, et sa bonne administration est un enjeu majeur de fiabilité et de sécurité pour les organisations.

---

**Fin du document.**
