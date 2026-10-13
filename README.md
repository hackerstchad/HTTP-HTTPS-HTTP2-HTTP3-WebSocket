# 🌐 GUIDE DU PROTOCOLES WEB AVANCÉS : HTTP, HTTPS, HTTP/2, HTTP/3 & WEBSOCKET

<img width="1248" height="832" alt="OIG3 4eFceoDC_31d" src="https://github.com/user-attachments/assets/67bc04d9-eb42-4510-8068-b9264a691b21" />


**Auteur :** HACKERS_TCHAD  
**Date de création :** 2026  
**Version :** 1.0 - Guide complet & avancé  
**Licence :** Éducation & Cybersécurité - HACKERS_TCHAD

---

##  TABLE DES MATIÈRES

1. [Introduction générale](#1-introduction-générale)
2. [Le protocole HTTP](#2-le-protocole-http)
3. [Le protocole HTTPS](#3-le-protocole-https)
4. [Le protocole HTTP/2](#4-le-protocole-http2)
5. [Le protocole HTTP/3](#5-le-protocole-http3)
6. [Le protocole WebSocket](#6-le-protocole-websocket)
7. [Comparatifs et différences](#7-comparatifs-et-différences)
8. [Architectures réseau](#8-architectures-réseau)
9. [Configurations serveur](#9-configurations-serveur)
10. [Outils de vérification Windows & Linux](#10-outils-de-vérification-windows--linux)
11. [Applications réelles](#11-applications-réelles)
12. [Simulateurs et labs](#12-simulateurs-et-labs)
13. [Sécurité offensive et défensive](#13-sécurité-offensive-et-défensive)
14. [Troubleshooting avancé](#14-troubleshooting-avancé)
15. [Références et crédits](#15-références-et-crédits)

---

# 1. INTRODUCTION GÉNÉRALE

## 1.1 Qu'est-ce qu'un protocole web ?

Un protocole web est un ensemble de règles et de conventions qui permettent à deux machines, généralement un client et un serveur, de communiquer sur un réseau informatique, en particulier sur Internet. Ces protocoles définissent le format des messages échangés, la manière dont ils sont transmis, la gestion des erreurs, l'authentification, le chiffrement et bien d'autres aspects essentiels au bon fonctionnement des services numériques modernes.

Les protocoles que nous allons étudier dans ce document — HTTP, HTTPS, HTTP/2, HTTP/3 et WebSocket — constituent la colonne vertébrale du World Wide Web et des applications temps réel. Ils ont été conçus à différentes époques pour répondre à des besoins évolutifs : du simple transfert de documents hypertextes aux applications interactives, en passant par le streaming, les jeux en ligne, la télémédecine, la finance en temps réel et l'Internet des objets.

## 1.2 Historique et évolution

L'histoire des protocoles web est intimement liée à celle d'Internet et du Web. Voici les grandes étapes :

- **1969 :** ARPANET, ancêtre d'Internet, utilise des protocoles expérimentaux.
- **1974 :** Vinton Cerf et Bob Kahn publient le protocole TCP/IP.
- **1989 :** Tim Berners-Lee, au CERN, propose le World Wide Web.
- **1991 :** Première version du protocole HTTP (HTTP/0.9).
- **1996 :** Publication de HTTP/1.0 (RFC 1945).
- **1997 :** HTTP/1.1 devient un standard (RFC 2068, puis RFC 2616).
- **2000 :** Le protocole WebSocket est conceptualisé, standardisé en 2011.
- **2015 :** HTTP/2 est publié en tant que RFC 7540.
- **2022 :** HTTP/3 est standardisé dans la RFC 9114.

Chaque version a apporté des améliorations en termes de performance, de sécurité, de latence et de prise en charge des applications modernes.

## 1.3 Pourquoi ce guide ?

Ce guide a pour objectif de fournir une compréhension approfondie, technique et pratique des principaux protocoles web. Il s'adresse aux étudiants, administrateurs système, développeurs, pentesteurs, chercheurs en cybersécurité et à toute personne souhaitant maîtriser les fondamentaux et les aspects avancés de la communication web. Vous y trouverez des définitions, des architectures, des configurations, des commandes de vérification, des applications réelles, des simulateurs et des cas d'usage concrets.

---

# 2. LE PROTOCOLE HTTP

## 2.1 Définition de HTTP

**HTTP (HyperText Transfer Protocol)** est un protocole de communication client-serveur utilisé pour transférer des données sur le Web. Il fonctionne selon un modèle requête/réponse : le client (généralement un navigateur web) envoie une requête à un serveur, qui répond en retournant une ressource (page HTML, image, fichier CSS, script JavaScript, vidéo, etc.).

HTTP est un protocole de la couche application du modèle OSI et de la couche application du modèle TCP/IP. Il repose généralement sur TCP (Transmission Control Protocol) et utilise le port 80 par défaut.

## 2.2 Caractéristiques principales de HTTP

HTTP présente les caractéristiques suivantes :

- **Sans état (stateless) :** Chaque requête est indépendante. Le serveur ne conserve pas d'informations sur les requêtes précédentes d'un même client.
- **Basé sur le texte :** Les requêtes et réponses sont lisibles par un humain (avant HTTP/2).
- **Extensible :** Les en-têtes permettent d'ajouter des fonctionnalités (authentification, cache, cookies, etc.).
- **Sans connexion persistante (HTTP/1.0) :** Une connexion TCP par ressource.
- **Connexions persistantes (HTTP/1.1) :** Réutilisation d'une même connexion TCP pour plusieurs requêtes.

## 2.3 Historique de HTTP

### 2.3.1 HTTP/0.9 (1991)

HTTP/0.9 est la première version du protocole. Elle est extrêmement simple :

- Une seule méthode : GET.
- Pas d'en-têtes.
- Pas de codes de statut.
- Réponse brute en HTML.

Exemple de requête HTTP/0.9 :

```
GET /
```

Exemple de réponse :

```html
<html>
  <body>Hello World</body>
</html>
```

### 2.3.2 HTTP/1.0 (1996)

HTTP/1.0 introduit :

- Plusieurs méthodes : GET, HEAD, POST.
- Les en-têtes de requête et de réponse.
- Les codes de statut (200, 404, 500, etc.).
- La notion de version du protocole.
- Le support des types MIME.

Cependant, chaque requête nécessite une nouvelle connexion TCP, ce qui est inefficace.

### 2.3.3 HTTP/1.1 (1997)

HTTP/1.1 est une version majeure qui introduit :

- **Connexions persistantes :** L'en-tête `Connection: keep-alive`.
- **Pipelining :** Envoi de plusieurs requêtes sans attendre les réponses.
- **Hôtes virtuels :** L'en-tête `Host` permet d'héberger plusieurs sites sur une même adresse IP.
- **Méthodes supplémentaires :** PUT, DELETE, OPTIONS, TRACE, CONNECT.
- **Gestion du cache :** En-têtes `Cache-Control`, `ETag`, `Last-Modified`.
- **Négociation de contenu :** En-têtes `Accept`, `Accept-Language`, `Accept-Encoding`.

HTTP/1.1 reste largement utilisé aujourd'hui, bien que HTTP/2 et HTTP/3 gagnent en popularité.

## 2.4 Structure d'une requête HTTP

Une requête HTTP/1.1 se compose de trois parties :

1. **Ligne de requête :** méthode, URI, version du protocole.
2. **En-têtes :** informations supplémentaires sur la requête.
3. **Corps (optionnel) :** données envoyées au serveur (formulaire, JSON, fichier, etc.).

Exemple de requête :

```http
GET /index.html HTTP/1.1
Host: www.example.com
User-Agent: Mozilla/5.0
Accept: text/html
Accept-Language: fr-FR
Connection: keep-alive
```

## 2.5 Structure d'une réponse HTTP

Une réponse HTTP/1.1 se compose de trois parties :

1. **Ligne de statut :** version du protocole, code de statut, message.
2. **En-têtes :** métadonnées sur la réponse.
3. **Corps (optionnel) :** contenu demandé.

Exemple de réponse :

```http
HTTP/1.1 200 OK
Date: Mon, 01 Jan 2026 12:00:00 GMT
Server: Apache/2.4.41
Content-Type: text/html; charset=UTF-8
Content-Length: 1234

<html>
  <body>Bienvenue sur example.com</body>
</html>
```

## 2.6 Méthodes HTTP

Les méthodes HTTP indiquent l'action que le client souhaite effectuer sur la ressource :

| Méthode | Description | Idempotente |
|---------|-------------|-------------|
| GET | Récupérer une ressource | Oui |
| HEAD | Récupérer les en-têtes sans le corps | Oui |
| POST | Envoyer des données au serveur | Non |
| PUT | Remplacer une ressource | Oui |
| DELETE | Supprimer une ressource | Oui |
| OPTIONS | Obtenir les options de communication | Oui |
| TRACE | Retourner la requête reçue (diagnostic) | Oui |
| CONNECT | Établir un tunnel (ex : HTTPS via proxy) | Non |
| PATCH | Modifier partiellement une ressource | Non |

## 2.7 Codes de statut HTTP

Les codes de statut sont regroupés en cinq classes :

### 2.7.1 1xx - Informationnel

| Code | Signification |
|------|---------------|
| 100 | Continue |
| 101 | Switching Protocols |
| 102 | Processing |
| 103 | Early Hints |

### 2.7.2 2xx - Succès

| Code | Signification |
|------|---------------|
| 200 | OK |
| 201 | Created |
| 202 | Accepted |
| 204 | No Content |
| 206 | Partial Content |

### 2.7.3 3xx - Redirection

| Code | Signification |
|------|---------------|
| 301 | Moved Permanently |
| 302 | Found |
| 304 | Not Modified |
| 307 | Temporary Redirect |
| 308 | Permanent Redirect |

### 2.7.4 4xx - Erreur client

| Code | Signification |
|------|---------------|
| 400 | Bad Request |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |
| 405 | Method Not Allowed |
| 408 | Request Timeout |
| 429 | Too Many Requests |

### 2.7.5 5xx - Erreur serveur

| Code | Signification |
|------|---------------|
| 500 | Internal Server Error |
| 501 | Not Implemented |
| 502 | Bad Gateway |
| 503 | Service Unavailable |
| 504 | Gateway Timeout |

## 2.8 En-têtes HTTP importants

### 2.8.1 En-têtes de requête

- **Host :** nom de domaine du serveur.
- **User-Agent :** identification du client.
- **Accept :** types de contenu acceptés.
- **Accept-Encoding :** encodages acceptés (gzip, deflate, br).
- **Accept-Language :** langues préférées.
- **Connection :** gestion de la connexion (keep-alive, close).
- **Content-Type :** type du corps de la requête.
- **Content-Length :** taille du corps.
- **Authorization :** informations d'authentification.
- **Cookie :** cookies envoyés au serveur.
- **Referer :** page d'origine de la requête.

### 2.8.2 En-têtes de réponse

- **Server :** logiciel serveur utilisé.
- **Date :** date et heure de la réponse.
- **Content-Type :** type du contenu retourné.
- **Content-Length :** taille du contenu.
- **Set-Cookie :** dépôt d'un cookie chez le client.
- **Location :** URL de redirection.
- **Cache-Control :** directives de cache.
- **Expires :** date d'expiration du contenu.
- **ETag :** identifiant de version de la ressource.
- **Last-Modified :** date de dernière modification.
- **WWW-Authenticate :** méthode d'authentification requise.

## 2.9 Gestion du cache HTTP

Le cache HTTP permet de stocker temporairement des réponses afin de réduire la latence et la charge du serveur. Les mécanismes principaux sont :

- **Expiration :** `Cache-Control: max-age=3600`, `Expires`.
- **Validation :** `ETag`, `Last-Modified`, requêtes conditionnelles (`If-None-Match`, `If-Modified-Since`).
- **Invalidation :** `Cache-Control: no-cache`, `no-store`, `must-revalidate`.

## 2.10 Cookies et sessions HTTP

HTTP étant stateless, les cookies permettent de maintenir l'état entre les requêtes. Un cookie est un petit fichier texte stocké par le navigateur et renvoyé au serveur à chaque requête. Il permet de gérer les sessions utilisateur, les préférences, le suivi publicitaire, etc.

Attributs de sécurité des cookies :

- **Secure :** cookie transmis uniquement en HTTPS.
- **HttpOnly :** cookie inaccessible via JavaScript.
- **SameSite :** protection contre les attaques CSRF (Strict, Lax, None).
- **Expires / Max-Age :** durée de vie du cookie.

## 2.11 Limites de HTTP/1.1

HTTP/1.1 souffre de plusieurs limitations :

- **Head-of-line blocking :** Une requête lente bloque les suivantes sur la même connexion.
- **Un seul flux par connexion TCP :** Impossibilité de multiplexage natif.
- **En-têtes répétés et verbeux :** Chaque requête répète les mêmes en-têtes.
- **Pas de compression des en-têtes :** Gaspiillage de bande passante.
- **Négociation TLS séparée :** Latence supplémentaire pour HTTPS.

Ces limites ont conduit au développement de HTTP/2 et HTTP/3.

## 2.12 Où utiliser HTTP

HTTP est utilisé partout sur Internet :

- Navigation web classique.
- APIs REST.
- Téléchargement de fichiers.
- Communication entre microservices.
- Services web SOAP.
- Applications mobiles (backend).
- IoT et capteurs connectés.
- Streaming vidéo basique.

## 2.13 Architecture typique HTTP

```
[Client : navigateur / curl / application]
                |
                | Requête HTTP (port 80)
                v
[Reverse proxy / Load balancer]
                |
                v
[Serveur web : Apache, Nginx, IIS]
                |
                v
[Application backend : PHP, Node.js, Python, Java, .NET]
                |
                v
[Base de données : MySQL, PostgreSQL, MongoDB, Redis]
```

## 2.14 Configuration basique d'un serveur HTTP

### 2.14.1 Apache HTTP Server

Fichier `/etc/apache2/sites-available/000-default.conf` :

```apache
<VirtualHost *:80>
    ServerName example.com
    DocumentRoot /var/www/html
    <Directory /var/www/html>
        AllowOverride All
        Require all granted
    </Directory>
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```

### 2.14.2 Nginx

Fichier `/etc/nginx/sites-available/default` :

```nginx
server {
    listen 80;
    server_name example.com;
    root /var/www/html;
    index index.html;

    location / {
        try_files $uri $uri/ =404;
    }
}
```

---

# 3. LE PROTOCOLE HTTPS

## 3.1 Définition de HTTPS

**HTTPS (HyperText Transfer Protocol Secure)** est la version sécurisée de HTTP. Il utilise HTTP comme protocole applicatif, mais il chiffre les communications grâce à une couche de sécurité basée sur TLS (Transport Layer Security) ou son prédécesseur SSL (Secure Sockets Layer). HTTPS utilise le port 443 par défaut.

L'objectif principal de HTTPS est de garantir :

- **Confidentialité :** Les données sont chiffrées et illisibles pour un attaquant interceptant le trafic.
- **Intégrité :** Les données ne peuvent pas être altérées en transit sans être détectées.
- **Authenticité :** Le client peut vérifier l'identité du serveur grâce à un certificat.

## 3.2 Historique de HTTPS

- **1994 :** Netscape développe SSL (Secure Sockets Layer) pour sécuriser HTTP.
- **1995 :** SSL 2.0 sort, rapidement suivi de SSL 3.0 en 1996.
- **1999 :** TLS 1.0 est publié (RFC 2246), basé sur SSL 3.0.
- **2006 :** TLS 1.1 (RFC 4346).
- **2008 :** TLS 1.2 (RFC 5246), version très répandue.
- **2018 :** TLS 1.3 (RFC 8446), plus rapide et plus sûr.
- **Depuis 2014 :** HTTPS devient un standard recommandé par Google et les principaux navigateurs.

## 3.3 Fonctionnement de HTTPS

HTTPS repose sur une poignée de main TLS/SSL avant l'échange de données HTTP. Les étapes principales sont :

1. **Résolution DNS :** Le client obtient l'adresse IP du serveur.
2. **Connexion TCP :** Le client établit une connexion TCP sur le port 443.
3. **Handshake TLS :**
   - Le client envoie un `ClientHello` avec les versions TLS, cipher suites et extensions supportées.
   - Le serveur répond avec un `ServerHello`, son certificat et les paramètres de la session.
   - Le client vérifie le certificat et échange les clés (selon la version TLS).
   - Les deux parties dérivent une clé de session symétrique.
4. **Communication chiffrée :** Les requêtes et réponses HTTP sont chiffrées avec la clé de session.

## 3.4 Les certificats SSL/TLS

Un certificat SSL/TLS est un fichier numérique qui lie une clé publique à une identité (nom de domaine, organisation). Il est délivré par une **Autorité de Certification (CA)** de confiance, sauf en cas de certificat auto-signé.

### 3.4.1 Types de certificats

- **Domain Validated (DV) :** Vérifie seulement le propriétaire du domaine.
- **Organization Validated (OV) :** Vérifie également l'organisation.
- **Extended Validation (EV) :** Vérification approfondie de l'entreprise.
- **Wildcard :** Couvre un domaine et tous ses sous-domaines.
- **SAN (Subject Alternative Name) :** Couvre plusieurs noms de domaine.
- **Self-signed :** Signé par son propre créateur, non reconnu par défaut.

### 3.4.2 Chaîne de confiance

La chaîne de confiance part du certificat du serveur, passe par les certificats intermédiaires, jusqu'au certificat racine installé dans le navigateur ou le système d'exploitation.

## 3.5 Cipher suites TLS

Une cipher suite est un ensemble d'algorithmes utilisés pour sécuriser une connexion TLS. Elle définit :

- L'algorithme d'échange de clés (ex : ECDHE).
- L'algorithme de signature (ex : RSA, ECDSA).
- L'algorithme de chiffrement symétrique (ex : AES-GCM, ChaCha20).
- La fonction de hachage (ex : SHA-256).

Exemple de cipher suite : `TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256`

## 3.6 TLS 1.3

TLS 1.3 apporte des améliorations majeures :

- Handshake plus rapide (souvent un seul aller-retour).
- Suppression des algorithmes obsolètes et vulnérables.
- Perfect Forward Secrecy (PFS) par défaut.
- Chiffrement des extensions du handshake.
- Meilleure résistance aux attaques (POODLE, BEAST, CRIME, etc.).

## 3.7 Avantages de HTTPS

- Protection contre l'écoute clandestine (Man-in-the-Middle).
- Authentification du serveur.
- Confiance des utilisateurs et des navigateurs.
- Amélioration du référencement naturel (SEO).
- Nécessaire pour HTTP/2 et HTTP/3 dans la plupart des navigateurs.
- Obligatoire pour les Progressive Web Apps, les paiements en ligne, les API sécurisées.

## 3.8 Limites et risques de HTTPS

- Nécessite un certificat valide (souvent payant ou renouvelé régulièrement).
- Consommation CPU plus élevée pour le chiffrement (marginale aujourd'hui).
- TLS peut mal être configuré (protocoles obsolètes, certificats expirés).
- HTTPS ne protège pas contre toutes les attaques (XSS, CSRF, injections).
- Certificats frauduleux ou autorités de certification compromises.

## 3.9 Où utiliser HTTPS

HTTPS doit être utilisé partout où la sécurité est nécessaire :

- Sites web publics et internes.
- APIs REST sécurisées.
- Applications bancaires et financières.
- Plateformes e-commerce.
- Services de messagerie.
- Réseaux sociaux.
- Intranets sensibles.
- Connexions IoT.
- Téléchargement de fichiers.

## 3.10 Architecture HTTPS

```
[Client navigateur]
        |
        | DNS resolution
        v
[CDN / WAF / Load balancer HTTPS]
        |
        | TLS termination
        v
[Reverse proxy HTTPS (Nginx, HAProxy, Traefik)]
        |
        | HTTP interne ou HTTPS
        v
[Application backend]
        |
        v
[Base de données]
```

## 3.11 Configuration HTTPS

### 3.11.1 Nginx avec Let's Encrypt

```nginx
server {
    listen 443 ssl http2;
    server_name example.com;
    root /var/www/html;

    ssl_certificate /etc/letsencrypt/live/example.com/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/example.com/privkey.pem;
    ssl_protocols TLSv1.2 TLSv1.3;
    ssl_ciphers 'ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES256-GCM-SHA384';
    ssl_prefer_server_ciphers off;
    ssl_session_cache shared:SSL:10m;
    ssl_session_timeout 1d;
}

server {
    listen 80;
    server_name example.com;
    return 301 https://$host$request_uri;
}
```

### 3.11.2 Apache avec TLS

```apache
<VirtualHost *:443>
    ServerName example.com
    DocumentRoot /var/www/html
    SSLEngine on
    SSLCertificateFile /etc/letsencrypt/live/example.com/cert.pem
    SSLCertificateKeyFile /etc/letsencrypt/live/example.com/privkey.pem
    SSLCertificateChainFile /etc/letsencrypt/live/example.com/chain.pem
    SSLProtocol all -SSLv3 -TLSv1 -TLSv1.1
    SSLCipherSuite HIGH:!aNULL:!MD5
</VirtualHost>
```

## 3.12 Renouvellement automatique Let's Encrypt

Let's Encrypt propose des certificats gratuits valables 90 jours. Le renouvellement est automatisé avec Certbot :

```bash
# Linux
sudo certbot renew --dry-run
```

---

# 4. LE PROTOCOLE HTTP/2

## 4.1 Définition de HTTP/2

**HTTP/2** est la deuxième version majeure du protocole HTTP, publiée en 2015 sous la RFC 7540. Il a été conçu pour améliorer les performances du Web sans modifier la sémantique de HTTP/1.1. HTTP/2 introduit le multiplexage, la compression des en-têtes, le server push et la priorisation des requêtes.

HTTP/2 repose sur un framing binaire et non plus sur du texte. Il nécessite généralement HTTPS dans les navigateurs modernes.

## 4.2 Historique de HTTP/2

- **2009 :** Google développe SPDY, un protocole expérimental pour améliorer HTTP.
- **2012 :** Le groupe de travail HTTPbis de l'IETF adopte SPDY comme base pour HTTP/2.
- **2015 :** Publication de HTTP/2 en tant que RFC 7540.
- **2020 :** RFC 7540 devient obsolète, remplacée par les RFC 9113 et 9114.

## 4.3 Caractéristiques de HTTP/2

### 4.3.1 Multiplexage

HTTP/2 permet d'envoyer plusieurs requêtes et réponses simultanément sur une seule connexion TCP. Cela résout le problème de head-of-line blocking au niveau applicatif de HTTP/1.1.

### 4.3.2 Compression des en-têtes (HPACK)

HPACK (Header Compression for HTTP/2) compresse les en-têtes répétitifs, réduisant la consommation de bande passante.

### 4.3.3 Server Push

Le serveur peut envoyer proactivement des ressources au client (CSS, JS) avant qu'elles ne soient demandées. Cependant, cette fonctionnalité est souvent désactivée car elle peut gaspiller la bande passante.

### 4.3.4 Priorisation des flux

Les clients peuvent indiquer l'importance relative des requêtes, permettant au serveur d'allouer les ressources réseau de manière optimale.

### 4.3.5 Framing binaire

Les messages HTTP/2 sont découpés en frames binaires, ce qui améliore l'efficacité du parsing et permet le multiplexage.

## 4.4 Structure d'une connexion HTTP/2

Une connexion HTTP/2 est composée de :

- **Connexion TCP :** sous-jacente, généralement sur TLS (port 443).
- **Streams :** canaux logiques bidirectionnels au sein de la connexion.
- **Messages :** requêtes ou réponses composées de frames.
- **Frames :** unités binaires de base (HEADERS, DATA, SETTINGS, etc.).

## 4.5 Types de frames HTTP/2

| Type de frame | Code | Description |
|---------------|------|-------------|
| DATA | 0x0 | Transporte le corps des messages |
| HEADERS | 0x1 | Transporte les en-têtes |
| PRIORITY | 0x2 | Définit la priorité d'un stream |
| RST_STREAM | 0x3 | Réinitialise un stream |
| SETTINGS | 0x4 | Paramètres de la connexion |
| PUSH_PROMISE | 0x5 | Annonce un server push |
| PING | 0x6 | Vérifie la latence |
| GOAWAY | 0x7 | Ferme la connexion proprement |
| WINDOW_UPDATE | 0x8 | Contrôle de flux |
| CONTINUATION | 0x9 | Continue les en-têtes fragmentés |

## 4.6 Avantages de HTTP/2

- Réduction de la latence perçue.
- Meilleure utilisation des connexions TCP.
- Réduction de la consommation de bande passante grâce à HPACK.
- Amélioration du chargement des pages riches en ressources.
- Compatibilité avec la sémantique HTTP/1.1.

## 4.7 Limites de HTTP/2

- Head-of-line blocking au niveau TCP : un paquet perdu bloque tous les streams.
- Complexité d'implémentation.
- Server push souvent mal utilisé ou désactivé.
- Nécessite généralement TLS (sauf en interne).
- Certains mécanismes de sécurité (HPACK) peuvent être vulnérables si mal implémentés.

## 4.8 Où utiliser HTTP/2

HTTP/2 est recommandé pour :

- Sites web modernes avec beaucoup de ressources.
- APIs REST haute performance.
- Applications mobiles.
- Streaming de données.
- Services nécessitant une faible latence.
- Microservices communiquant sur des connexions longues.

## 4.9 Architecture HTTP/2

```
[Client]
   |
   | TLS + ALPN (h2)
   v
[Reverse proxy HTTP/2 : Nginx, HAProxy, Envoy]
   |
   | HTTP/2 ou HTTP/1.1 interne
   v
[Backend]
```

## 4.10 Configuration HTTP/2

### 4.10.1 Nginx

```nginx
server {
    listen 443 ssl http2;
    server_name example.com;
    ssl_certificate /path/to/cert.pem;
    ssl_certificate_key /path/to/key.pem;
    # HTTP/2 est activé par 'http2' dans listen
}
```

### 4.10.2 Apache

```apache
Protocols h2 http/1.1

<VirtualHost *:443>
    ServerName example.com
    SSLEngine on
    SSLCertificateFile /path/to/cert.pem
    SSLCertificateKeyFile /path/to/key.pem
</VirtualHost>
```

## 4.11 Négociation HTTP/2

HTTP/2 peut être négocié de deux manières :

- **Sur TLS :** via l'extension ALPN (Application-Layer Protocol Negotiation). Le client propose `h2`, le serveur accepte.
- **En clair :** via la mise à niveau HTTP/1.1 (`Upgrade: h2c`). Peu utilisé sur Internet.

---

# 5. LE PROTOCOLE HTTP/3

## 5.1 Définition de HTTP/3

**HTTP/3** est la dernière version majeure du protocole HTTP, publiée en 2022 sous la RFC 9114. Contrairement à ses prédécesseurs, HTTP/3 ne repose pas sur TCP mais sur **QUIC (Quick UDP Internet Connections)**, un protocole de transport développé par Google et standardisé par l'IETF.

HTTP/3 vise à résoudre le head-of-line blocking au niveau TCP de HTTP/2 et à réduire encore la latence des connexions web.

## 5.2 Historique de HTTP/3

- **2012 :** Google développe QUIC initialement sur UDP.
- **2015 :** QUIC est proposé à l'IETF.
- **2018 :** HTTP-over-QUIC est renommé HTTP/3.
- **2021 :** Publication de QUIC en tant que RFC 9000.
- **2022 :** Standardisation de HTTP/3 dans la RFC 9114.

## 5.3 Caractéristiques de HTTP/3

### 5.3.1 Transport sur QUIC/UDP

HTTP/3 utilise QUIC, qui repose sur UDP (User Datagram Protocol) au lieu de TCP. Cela permet une connexion plus rapide et une meilleure résilience aux pertes de paquets.

### 5.3.2 Intégration native de TLS 1.3

Dans HTTP/3, TLS 1.3 est intégré à QUIC. Le handshake QUIC et le handshake TLS sont combinés, réduisant la latence initiale.

### 5.3.3 Multiplexage sans head-of-line blocking

Chaque stream QUIC est indépendant. La perte d'un paquet n'affecte pas les autres streams, contrairement à HTTP/2 sur TCP.

### 5.3.4 Migration de connexion

QUIC utilise un identifiant de connexion unique. Un client peut changer d'adresse IP (ex : WiFi vers 4G) sans interrompre la connexion.

### 5.3.5 Contrôle de flux amélioré

QUIC gère le contrôle de flux au niveau de la connexion et au niveau de chaque stream.

## 5.4 Structure d'une connexion HTTP/3

```
[Application HTTP/3]
        |
        | QUIC
        v
[TLS 1.3 intégré]
        |
        | UDP
        v
[Réseau IP]
```

## 5.5 Avantages de HTTP/3

- Latence initiale réduite grâce au 0-RTT et au handshake combiné.
- Meilleure performance sur les réseaux mobiles et instables.
- Résilience aux changements d'IP.
- Pas de head-of-line blocking au niveau transport.
- Sécurité renforcée par TLS 1.3.

## 5.6 Limites de HTTP/3

- Maturité encore en cours pour certains équipements réseau.
- Certains pare-feu bloquent UDP ou le QoS le dégrade.
- Complexité d'implémentation.
- Adoption encore partielle chez les fournisseurs d'accès.
- Débogage plus complexe que TCP.

## 5.7 Où utiliser HTTP/3

HTTP/3 est particulièrement utile pour :

- Applications mobiles et roaming.
- Streaming vidéo en direct.
- Jeux en ligne.
- Services temps réel.
- Réseaux à forte latence ou pertes de paquets.
- CDN modernes (Cloudflare, Fastly, Akamai).

## 5.8 Architecture HTTP/3

```
[Client QUIC-compatible]
        |
        | UDP port 443 + QUIC
        v
[Load balancer UDP/QUIC]
        |
        v
[Reverse proxy HTTP/3 : Nginx, HAProxy, Caddy, LiteSpeed]
        |
        v
[Backend HTTP/1.1, HTTP/2 ou HTTP/3]
```

## 5.9 Configuration HTTP/3

### 5.9.1 Nginx (module nginx-quic)

```nginx
server {
    listen 443 quic reuseport;
    listen 443 ssl;
    server_name example.com;

    ssl_certificate /path/to/cert.pem;
    ssl_certificate_key /path/to/key.pem;
    ssl_protocols TLSv1.3;

    add_header Alt-Svc 'h3=":443"; ma=86400';
}
```

### 5.9.2 Caddy

Caddy supporte HTTP/3 nativement :

```caddyfile
example.com {
    tls /path/to/cert.pem /path/to/key.pem
    respond "Hello HTTP/3"
}
```

### 5.9.3 Cloudflare

Cloudflare active HTTP/3 automatiquement pour les domaines proxysés. Il suffit de cocher l'option dans le tableau de bord.

## 5.10 Négociation HTTP/3

HTTP/3 est annoncé via l'en-tête `Alt-Svc` (Alternative Service) renvoyé par le serveur. Le client tente ensuite de se connecter en QUIC sur le port indiqué. Si la connexion QUIC réussit, les futures requêtes utilisent HTTP/3.

Exemple d'en-tête :

```http
Alt-Svc: h3=":443"; ma=86400
```

---

# 6. LE PROTOCOLE WEBSocket

## 6.1 Définition de WebSocket

**WebSocket** est un protocole de communication bidirectionnelle en temps réel entre un client et un serveur. Contrairement à HTTP, où le client doit initier chaque échange, WebSocket permet une connexion persistante et full-duplex : le client et le serveur peuvent envoyer des messages à tout moment.

WebSocket est standardisé dans la RFC 6455 et utilise généralement le port 80 (ws://) ou 443 (wss://).

## 6.2 Historique de WebSocket

- **2008 :** Michael Carter et Ian Hickson proposent le concept.
- **2010 :** Premières implémentations expérimentales dans Chrome.
- **2011 :** Standardisation dans la RFC 6455.
- **Années 2010 :** Adoption massive par les applications temps réel.
- **Aujourd'hui :** Utilisé dans le chat, les jeux, le trading, la collaboration en ligne, etc.

## 6.3 Fonctionnement de WebSocket

Le protocole WebSocket démarre par une requête HTTP classique contenant un en-tête `Upgrade` :

```http
GET /chat HTTP/1.1
Host: example.com
Upgrade: websocket
Connection: Upgrade
Sec-WebSocket-Key: dGhlIHNhbXBsZSBub25jZQ==
Sec-WebSocket-Version: 13
```

Si le serveur accepte, il répond :

```http
HTTP/1.1 101 Switching Protocols
Upgrade: websocket
Connection: Upgrade
Sec-WebSocket-Accept: s3pPLMBiTxaQ9kYGzzhZRbK+xOo=
```

Ensuite, la connexion reste ouverte et les messages peuvent circuler dans les deux sens sous forme de frames WebSocket.

## 6.4 Caractéristiques de WebSocket

- **Full-duplex :** Communication simultanée dans les deux sens.
- **Faible latence :** Pas de réétablissement de connexion à chaque message.
- **Léger :** En-têtes de frame réduits après le handshake.
- **Basé sur TCP :** WebSocket repose sur TCP, pas sur UDP.
- **Sécurisable :** WSS (WebSocket Secure) utilise TLS.

## 6.5 Types de frames WebSocket

| Opcode | Type | Description |
|--------|------|-------------|
| 0x0 | Continuation | Suite d'un message fragmenté |
| 0x1 | Text | Message texte |
| 0x2 | Binary | Message binaire |
| 0x8 | Close | Fermeture de la connexion |
| 0x9 | Ping | Vérification de la vivacité |
| 0xA | Pong | Réponse à un ping |

## 6.6 Avantages de WebSocket

- Communication temps réel.
- Réduction de la surcharge réseau par rapport au polling HTTP.
- Idéal pour les applications interactives.
- Support natif par les navigateurs modernes.
- Simplicité d'utilisation côté client avec l'API JavaScript WebSocket.

## 6.7 Limites de WebSocket

- Connexions persistantes consomment des ressources serveur.
- Moins adapté aux communications unidirectionnelles simples.
- Certains proxies et pare-feu peuvent bloquer WebSocket.
- Gestion complexe de la scalabilité (load balancing sticky sessions).
- Risques de sécurité si le handshake et les messages ne sont pas validés.

## 6.8 Où utiliser WebSocket

WebSocket est utilisé dans de nombreux cas d'usage :

- Messageries instantanées et chat.
- Jeux multijoueurs en temps réel.
- Plateformes de trading financier.
- Tableaux de bord temps réel.
- Collaboration en ligne (Google Docs, Figma).
- Streaming de données (capteurs, IoT).
- Notifications push.
- Vidéoconférence (signaling).
- Télémédecine.

## 6.9 Architecture WebSocket

```
[Client navigateur / application mobile]
        |
        | WSS (WebSocket Secure)
        v
[Load balancer avec sticky sessions]
        |
        v
[Serveur WebSocket : Node.js, Socket.io, ws, aiohttp]
        |
        v
[Broker de messages : Redis, RabbitMQ, Kafka] (optionnel)
        |
        v
[Cluster de serveurs WebSocket]
```

## 6.10 Configuration WebSocket

### 6.10.1 Nginx reverse proxy WebSocket

```nginx
map $http_upgrade $connection_upgrade {
    default upgrade;
    '' close;
}

server {
    listen 443 ssl;
    server_name ws.example.com;

    location /ws {
        proxy_pass http://backend:3000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection $connection_upgrade;
        proxy_set_header Host $host;
        proxy_read_timeout 86400;
    }
}
```

### 6.10.2 Apache reverse proxy WebSocket

```apache
<VirtualHost *:443>
    ServerName ws.example.com
    SSLEngine on
    SSLCertificateFile /path/to/cert.pem
    SSLCertificateKeyFile /path/to/key.pem

    ProxyPass /ws ws://backend:3000/ws
    ProxyPassReverse /ws ws://backend:3000/ws

    RewriteEngine on
    RewriteCond %{HTTP:Upgrade} websocket [NC]
    RewriteRule ^/?(.*) "ws://backend:3000/$1" [P,L]
</VirtualHost>
```

## 6.11 Exemple de serveur WebSocket en Node.js

```javascript
const WebSocket = require('ws');
const wss = new WebSocket.Server({ port: 3000 });

wss.on('connection', function connection(ws) {
    ws.on('message', function incoming(message) {
        console.log('received: %s', message);
    });
    ws.send('Bienvenue sur le serveur WebSocket !');
});
```

---

# 7. COMPARATIFS ET DIFFÉRENCES

## 7.1 Tableau comparatif général

| Caractéristique | HTTP/1.1 | HTTPS | HTTP/2 | HTTP/3 | WebSocket |
|-----------------|----------|-------|--------|--------|-----------|
| Couche transport | TCP | TCP + TLS | TCP + TLS | QUIC/UDP | TCP |
| Port par défaut | 80 | 443 | 443 | 443 | 80/443 |
| Chiffrement | Non | Oui (TLS) | Souvent TLS | TLS 1.3 intégré | Optionnel (WSS) |
| Multiplexage | Non | Non | Oui | Oui | Oui (connexion unique) |
| Compression en-têtes | Non | Non | Oui (HPACK) | Oui (QPACK) | Non |
| Bidirectionnel | Non | Non | Non | Non | Oui |
| Latence | Élevée | Élevée | Moyenne | Faible | Très faible |
| Head-of-line blocking TCP | Oui | Oui | Oui | Non | Oui |
| Utilisation typique | Sites simples | Sites sécurisés | Sites modernes | Mobiles, streaming | Temps réel |

## 7.2 Différences entre HTTP et WebSocket

HTTP est un protocole requête/réponse stateless, tandis que WebSocket établit une connexion persistante full-duplex. HTTP est adapté au transfert de ressources et aux APIs, WebSocket aux applications temps réel.

## 7.3 Différences entre HTTP/2 et HTTP/3

HTTP/2 et HTTP/3 partagent la sémantique HTTP et le multiplexage, mais HTTP/2 utilise TCP et HTTP/3 utilise QUIC sur UDP. HTTP/3 résout le head-of-line blocking au niveau transport et intègre TLS 1.3 nativement.

---

# 8. ARCHITECTURES RÉSEAU

## 8.1 Architecture classique web

```
Internet
   |
   v
Firewall
   |
   v
CDN / WAF
   |
   v
Load Balancer (L4/L7)
   |
   +--> Reverse Proxy (Nginx / HAProxy / Traefik)
            |
            +--> Web Server Pool
                     |
                     +--> Application Server
                              |
                              +--> Database
                              +--> Cache (Redis/Memcached)
                              +--> Message Queue
```

## 8.2 Architecture microservices

```
API Gateway
   |
   +--> Service A (HTTP/REST)
   +--> Service B (gRPC)
   +--> Service C (WebSocket)
   +--> Service D (HTTP/2 streaming)
   |
Service Mesh (Envoy, Istio)
   |
Kubernetes Cluster
```

## 8.3 Architecture temps réel

```
[Clients Web/Mobile]
        |
        | WSS
        v
[Load Balancer sticky]
        |
        v
[WebSocket Cluster]
        |
        +--> Redis Pub/Sub
        +--> RabbitMQ
        +--> Kafka
        |
        v
[Backend Services]
```

---

# 9. CONFIGURATIONS SERVEUR

## 9.1 Nginx complet (HTTP, HTTPS, HTTP/2, WebSocket)

```nginx
server {
    listen 80;
    server_name example.com;
    return 301 https://$host$request_uri;
}

server {
    listen 443 ssl http2;
    listen 443 quic reuseport;
    server_name example.com;

    ssl_certificate /etc/letsencrypt/live/example.com/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/example.com/privkey.pem;
    ssl_protocols TLSv1.2 TLSv1.3;
    ssl_prefer_server_ciphers off;

    add_header Alt-Svc 'h3=":443"; ma=86400';

    location / {
        proxy_pass http://backend:8080;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }

    location /ws {
        proxy_pass http://backend:3000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
        proxy_read_timeout 86400;
    }
}
```

## 9.2 Apache complet

```apache
<VirtualHost *:80>
    ServerName example.com
    Redirect permanent / https://example.com/
</VirtualHost>

<VirtualHost *:443>
    ServerName example.com
    Protocols h2 http/1.1
    SSLEngine on
    SSLCertificateFile /path/to/cert.pem
    SSLCertificateKeyFile /path/to/key.pem

    ProxyPass / http://backend:8080/
    ProxyPassReverse / http://backend:8080/

    RewriteEngine on
    RewriteCond %{HTTP:Upgrade} websocket [NC]
    RewriteRule ^/?(.*) "ws://backend:3000/$1" [P,L]
</VirtualHost>
```

## 9.3 Caddy complet

```caddyfile
example.com {
    tls /path/to/cert.pem /path/to/key.pem

    reverse_proxy /ws backend:3000
    reverse_proxy /* backend:8080
}
```

## 9.4 HAProxy

```haproxy
global
    maxconn 4096

defaults
    mode http
    timeout connect 5s
    timeout client 30s
    timeout server 30s

frontend https_frontend
    bind *:443 ssl crt /path/to/cert.pem alpn h2,http/1.1
    default_backend web_servers

backend web_servers
    server web1 192.168.1.10:8080 check
    server web2 192.168.1.11:8080 check
```

## 9.5 Traefik

```yaml
http:
  routers:
    myrouter:
      rule: "Host(`example.com`)"
      service: myservice
      tls:
        certResolver: letsencrypt
  services:
    myservice:
      loadBalancer:
        servers:
          - url: "http://backend:8080"
```

---

# 10. OUTILS DE VÉRIFICATION WINDOWS & LINUX

## 10.1 Vérifier le protocole HTTP supporté par un serveur

### 10.1.1 Linux/macOS avec curl

```bash
curl -I --http2 https://example.com
curl -I --http3 https://example.com
```

### 10.1.2 Windows avec PowerShell

```powershell
Invoke-WebRequest -Uri https://example.com -Method HEAD
```

## 10.2 Tester HTTP/2

### 10.2.1 curl avec HTTP/2

```bash
curl -I --http2 https://example.com
```

### 10.2.2 nghttp

```bash
nghttp -nv https://example.com
```

### 10.2.3 h2spec

```bash
h2spec -h example.com -p 443 -t
```

### 10.2.4 Outils en ligne

- https://tools.keycdn.com/http2-test
- https://www.ssllabs.com/ssltest/

## 10.3 Tester HTTP/3

### 10.3.1 curl avec support HTTP/3

```bash
curl --http3 -I https://example.com
```

### 10.3.2 ngtcp2 / quiche client

```bash
./client example.com 443
```

### 10.3.3 Chrome / Firefox Developer Tools

Dans l'onglet Réseau, ajoutez la colonne "Protocol" pour voir h2, h3, etc.

### 10.3.4 Outils en ligne

- https://http3check.net/
- https://www.cloudflare.com/http3/

## 10.4 Tester WebSocket

### 10.4.1 wscat (Node.js)

```bash
npm install -g wscat
wscat -c wss://echo.websocket.org
```

### 10.4.2 websocat

```bash
websocat wss://echo.websocket.org
```

### 10.4.3 curl avec upgrade WebSocket

```bash
curl -i -N \
  -H "Connection: Upgrade" \
  -H "Upgrade: websocket" \
  -H "Sec-WebSocket-Key: $(openssl rand -base64 16)" \
  -H "Sec-WebSocket-Version: 13" \
  https://example.com/ws
```

### 10.4.4 Python

```python
import websocket
ws = websocket.create_connection("wss://echo.websocket.org")
ws.send("Hello")
print(ws.recv())
ws.close()
```

## 10.5 Vérifier TLS/SSL

### 10.5.1 openssl

```bash
openssl s_client -connect example.com:443 -tls1_3
openssl s_client -connect example.com:443 -servername example.com
```

### 10.5.2 nmap

```bash
nmap --script ssl-enum-ciphers -p 443 example.com
```

### 10.5.3 testssl.sh

```bash
./testssl.sh https://example.com
```

### 10.5.4 sslyze

```bash
sslyze --regular example.com
```

### 10.5.5 Windows : Inspecteur de certificat

- Double-cliquez sur le cadenas dans le navigateur.
- Utilisez PowerShell : `Get-TlsCipherSuite`

## 10.6 Analyse de trafic réseau

### 10.6.1 tcpdump

```bash
sudo tcpdump -i eth0 port 80 -w http.pcap
sudo tcpdump -i eth0 port 443 -w https.pcap
```

### 10.6.2 Wireshark

Wireshark permet de capturer et décoder HTTP, HTTP/2, QUIC, TLS et WebSocket.

### 10.6.3 tshark

```bash
tshark -i eth0 -Y http -T fields -e http.host -e http.request.uri
```

### 10.6.4 netsh (Windows)

```cmd
netsh trace start capture=yes tracefile=c:\temp\network.etl
netsh trace stop
```

## 10.7 Vérifier les ports et connexions

### 10.7.1 Linux

```bash
ss -tuln | grep -E '80|443'
netstat -tuln | grep -E '80|443'
lsof -i :443
```

### 10.7.2 Windows

```cmd
netstat -an | findstr "443"
Get-NetTCPConnection -LocalPort 443
Test-NetConnection -ComputerName example.com -Port 443
```

## 10.8 Vérifier DNS

### 10.8.1 Linux

```bash
nslookup example.com
dig example.com +short
host example.com
```

### 10.8.2 Windows

```cmd
nslookup example.com
Resolve-DnsName example.com
```

## 10.9 Benchmarks et tests de charge

### 10.9.1 Apache Bench (ab)

```bash
ab -n 1000 -c 100 https://example.com/
```

### 10.9.2 wrk

```bash
wrk -t12 -c400 -d30s https://example.com/
```

### 10.9.3 hey

```bash
hey -n 1000 -c 50 https://example.com/
```

### 10.9.4 k6

```bash
k6 run --vus 50 --duration 30s script.js
```

### 10.9.5 Artillery

```bash
artillery quick --count 100 --num 10 https://example.com/
```

### 10.9.6 JMeter

JMeter permet de simuler des milliers d'utilisateurs HTTP, HTTPS et WebSocket.

## 10.10 Commandes Windows complètes

```powershell
# Tester une connexion HTTPS
Invoke-WebRequest -Uri https://example.com -UseBasicParsing

# Voir les cipher suites supportés
Get-TlsCipherSuite | Format-Table Name,Certificate

# Capturer les paquets
netsh trace start capture=yes tracefile=c:\trace.etl

# Résoudre un nom DNS
Resolve-DnsName example.com

# Tester un port
Test-NetConnection -ComputerName example.com -Port 443

# Voir les certificats installés
Get-ChildItem -Path Cert:\LocalMachine\Root

# Utiliser curl natif Windows
curl.exe -I https://example.com
```

## 10.11 Commandes Linux complètes

```bash
# Tester une connexion HTTPS
curl -I https://example.com

# Voir les cipher suites supportées
openssl ciphers -v 'ALL:COMPLEMENTOFALL'

# Capturer les paquets
sudo tcpdump -i any port 443 -w capture.pcap

# Résoudre un nom DNS
dig example.com ANY +short

# Tester un port
nc -zv example.com 443

# Voir les certificats installés
ls /etc/ssl/certs/

# Vérifier HTTP/2
curl -I --http2 https://example.com

# Vérifier HTTP/3
curl --http3 -I https://example.com

# Vérifier WebSocket
wscat -c wss://echo.websocket.org
```

---

# 11. APPLICATIONS RÉELLES

## 11.1 Applications utilisant HTTP/1.1

- Sites web statiques legacy.
- APIs REST traditionnelles.
- Intégrations avec anciens systèmes.
- Outils de monitoring simples.
- Téléchargements FTP-like via HTTP.

## 11.2 Applications utilisant HTTPS

- Tous les sites web modernes.
- E-commerce (Amazon, eBay).
- Banques en ligne.
- Réseaux sociaux (Facebook, Twitter, LinkedIn).
- Messageries (Gmail, Outlook Web).
- Cloud providers (AWS, Azure, GCP consoles).

## 11.3 Applications utilisant HTTP/2

- Sites à fort trafic (Google, YouTube, Facebook).
- APIs modernes (GitHub API, Twitter API v2).
- Applications mobiles (iOS, Android).
- CDN (Cloudflare, Akamai, Fastly).
- Dashboards riches en ressources.

## 11.4 Applications utilisant HTTP/3

- YouTube, Facebook, Netflix (expérimentations).
- Cloudflare (activé par défaut).
- Google Search.
- Applications mobiles sur réseaux instables.
- Jeux en ligne et streaming.

## 11.5 Applications utilisant WebSocket

- WhatsApp Web, Messenger.
- Slack, Discord.
- Zoom, Google Meet (signaling).
- Plateformes de trading (Bloomberg, eToro).
- Jeux en ligne (Agar.io, Slither.io).
- Tableaux de bord temps réel (Grafana Live).
- IoT et supervision industrielle.

---

# 12. SIMULATEURS ET LABS

## 12.1 Simulateurs HTTP/HTTPS

- **Postman :** Tests d'API HTTP/HTTPS.
- **Insomnia :** Alternative légère à Postman.
- **httpbin.org :** Service de test HTTP.
- **Wireshark :** Analyse de paquets.
- **Burp Suite :** Proxy d'interception HTTP/HTTPS.
- **OWASP ZAP :** Scanner de sécurité web.

## 12.2 Simulateurs HTTP/2

- **nghttp2.org :** Serveur et client HTTP/2.
- **h2spec :** Suite de tests de conformité HTTP/2.
- **curl :** Support natif HTTP/2.
- **Chrome DevTools :** Visualisation du protocole.

## 12.3 Simulateurs HTTP/3

- **quiche (Cloudflare) :** Implémentation QUIC/HTTP/3.
- **ngtcp2 :** Implémentation QUIC.
- **aioquic :** Implémentation Python QUIC/HTTP/3.
- **http3check.net :** Test en ligne.
- **Chrome Canary / Firefox Nightly :** Navigateurs expérimentaux.

## 12.4 Simulateurs WebSocket

- **wscat :** Client/serveur WebSocket en ligne de commande.
- **websocat :** Outil avancé de manipulation WebSocket.
- **echo.websocket.org :** Serveur d'écho WebSocket public.
- **Socket.io :** Framework client/serveur temps réel.
- **Pie Socket :** Service WebSocket cloud.
- **Pusher :** Service de notifications temps réel.

## 12.5 Labs complets

- **Vagrant + VirtualBox :** Créer des labs locaux.
- **Docker Compose :** Déployer Nginx, Apache, Node.js, Redis.
- **Kubernetes :** Labs de scalabilité et load balancing.
- **Mininet :** Simulation de réseaux SDN.
- **GNS3 / Packet Tracer :** Simulation réseau avancée.

---

# 13. SÉCURITÉ OFFENSIVE ET DÉFENSIVE

## 13.1 Menaces communes

- **Man-in-the-Middle (MITM) :** Interception du trafic non chiffré.
- **SSL/TLS stripping :** Forçage vers HTTP non sécurisé.
- **Downgrade attacks :** Forçage vers TLS 1.0/1.1.
- **HPACK/RCE :** Exploitation de vulnérabilités HTTP/2.
- **WebSocket injection :** Envoi de messages non autorisés.
- **Cross-Site WebSocket Hijacking (CSWSH) :** Usurpation de connexion WebSocket.
- **DoS :** Saturation de connexions HTTP/2 ou WebSocket.

## 13.2 Bonnes pratiques défensives

- Forcer HTTPS avec HSTS.
- Désactiver TLS 1.0 et 1.1.
- Utiliser TLS 1.3 dès que possible.
- Configurer correctement les cipher suites.
- Activer HPKP/CT (selon le contexte).
- Valider toutes les entrées côté serveur.
- Authentifier les connexions WebSocket.
- Limiter le nombre de connexions par IP.
- Surveiller les logs et le trafic anormal.
- Maintenir les serveurs et bibliothèques à jour.

## 13.3 Outils de sécurité

- **Burp Suite :** Test de sécurité web.
- **OWASP ZAP :** Scanner open source.
- **Nmap :** Scan de ports et services.
- **Nikto :** Scanner de vulnérabilités web.
- **SQLMap :** Tests d'injection SQL.
- **Metasploit :** Exploitation et tests de intrusion.
- **Wireshark :** Analyse forensique.
- **Bettercap :** MITM, sniffing, spoofing.

---

# 14. TROUBLESHOOTING AVANCÉ

## 14.1 Problèmes HTTP/1.1

- Lenteur due aux connexions non persistantes.
- Head-of-line blocking.
- En-têtes trop volumineux.
- Mauvaise configuration du cache.

## 14.2 Problèmes HTTPS

- Certificat expiré ou invalide.
- Chaîne de confiance incomplète.
- Protocoles TLS obsolètes.
- SNI mal configuré.
- HSTS incorrect.

## 14.3 Problèmes HTTP/2

- ALPN non supporté.
- Server push mal configuré.
- Incompatibilité avec certains proxies.
- Head-of-line blocking TCP.

## 14.4 Problèmes HTTP/3

- UDP bloqué par le pare-feu.
- QUIC mal supporté par le client.
- Certificat incompatible avec TLS 1.3.
- Load balancer ne gérant pas UDP.

## 14.5 Problèmes WebSocket

- Proxy bloquant l'upgrade.
- Timeout de connexion.
- Load balancer sans sticky sessions.
- Fuite de ressources serveur.
- Messages non validés.

## 14.6 Commandes de diagnostic

```bash
# Vérifier les en-têtes
curl -I -v https://example.com

# Vérifier la chaîne de certificats
openssl s_client -connect example.com:443 -showcerts

# Tester la résolution DNS
dig +trace example.com

# Vérifier la connectivité réseau
mtr example.com

# Analyser les performances
curl -o /dev/null -w "%{time_total}\n" https://example.com

# Vérifier les logs serveur
sudo tail -f /var/log/nginx/access.log
sudo tail -f /var/log/apache2/error.log
```

---

# 15. RÉFÉRENCES ET CRÉDITS

## 15.1 RFCs officielles

- RFC 1945 - HTTP/1.0
- RFC 2068 / RFC 2616 / RFC 7230-7235 - HTTP/1.1
- RFC 7540 / RFC 9113 - HTTP/2
- RFC 9114 - HTTP/3
- RFC 6455 - WebSocket
- RFC 8446 - TLS 1.3
- RFC 9000 - QUIC

## 15.2 Crédits

**Auteur :** HACKERS_TCHAD  
**Date de création :** 2026  
**Objectif :** Éducation, cybersécurité et administration réseau.

## 15.3 Remerciements

- IETF pour les standards ouverts.
- Apache Software Foundation et Nginx Inc.
- Cloudflare pour les avancées sur HTTP/3/QUIC.
- Google pour QUIC, SPDY et Chrome.
- Mozilla pour Firefox et les outils de développement.
- La communauté open source pour les outils de test et d'analyse.

---

# ANNEXE A : GLOSSAIRE

- **ALPN :** Application-Layer Protocol Negotiation.
- **CA :** Certificate Authority (Autorité de Certification).
- **CDN :** Content Delivery Network.
- **CSRF :** Cross-Site Request Forgery.
- **HPACK :** Header Compression for HTTP/2.
- **HSTS :** HTTP Strict Transport Security.
- **MITM :** Man-in-the-Middle.
- **PFS :** Perfect Forward Secrecy.
- **QUIC :** Quick UDP Internet Connections.
- **SNI :** Server Name Indication.
- **TLS :** Transport Layer Security.
- **WAF :** Web Application Firewall.
- **WSS :** WebSocket Secure.
- **XSS :** Cross-Site Scripting.

---

# ANNEXE B : COMMANDES RÉCAPITULATIVES

## Linux/macOS

```bash
# HTTP
curl -I http://example.com

# HTTPS
curl -I https://example.com
openssl s_client -connect example.com:443

# HTTP/2
curl -I --http2 https://example.com
nghttp -nv https://example.com

# HTTP/3
curl --http3 -I https://example.com

# WebSocket
wscat -c wss://echo.websocket.org
websocat wss://echo.websocket.org

# Scanner TLS
nmap --script ssl-enum-ciphers -p 443 example.com
./testssl.sh https://example.com

# Capture
tshark -i eth0 -Y http
sudo tcpdump -i eth0 port 443 -w capture.pcap
```

## Windows

```powershell
# HTTP/HTTPS
Invoke-WebRequest -Uri https://example.com -UseBasicParsing
curl.exe -I https://example.com

# TLS
Get-TlsCipherSuite
Get-ChildItem -Path Cert:\LocalMachine\Root

# Réseau
Test-NetConnection -ComputerName example.com -Port 443
Resolve-DnsName example.com
netsh trace start capture=yes tracefile=c:\trace.etl
```

---

# ANNEXE C : EXEMPLES DE CONFIGURATION DOCKER

```yaml
version: '3.8'
services:
  nginx:
    image: nginx:alpine
    ports:
      - "80:80"
      - "443:443"
    volumes:
      - ./nginx.conf:/etc/nginx/nginx.conf
      - ./certs:/etc/nginx/certs
  backend:
    image: node:18-alpine
    working_dir: /app
    volumes:
      - ./backend:/app
    command: node server.js
  redis:
    image: redis:alpine
```

---

# ANNEXE D : LIENS UTILES

- https://developer.mozilla.org/fr/docs/Web/HTTP
- https://httpwg.org/
- https://datatracker.ietf.org/
- https://www.cloudflare.com/learning/
- https://letsencrypt.org/
- https://owasp.org/
- https://www.ssllabs.com/ssltest/
- https://http3check.net/

---

**FIN DU DOCUMENT**

*Document rédigé par HACKERS_TCHAD en 2026. Utilisation à des fins éducatives et professionnelles.*
