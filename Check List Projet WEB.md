# Check List Projet WEB - Plan B

> **Projet** : Plan B - Plateforme immobilière  
> **Stack** : React (Frontend) + Symfony/PHP (Backend) + PostgreSQL (BDD)  
> **Date** : Janvier 2026

---

## Projet (Organisation)

| Critère | Statut | Détails |
|---------|--------|---------|
| **Git (GitHub, GitLab)** | ✅ Fait | Repository GitHub avec structure complète |
| **GitHub Action** | ✅ Fait | Workflow CI/CD configuré (`npm-publish-github-packages.yml`) |
| **Gestion des tâches (Trello, Jira, GitHub issues...)** | ⚠️ À améliorer | Pas d'outil de gestion de tâches visible |
| **Diagramme (GANTT, MCD, UML...)** | ⚠️ À améliorer | Pas de diagrammes formels dans le repo |
| **MockUp (Figma, Canva, Stitch...)** | ⚠️ À améliorer | Pas de lien vers mockups dans la documentation |

---

## BDD

| Critère | Statut | Détails |
|---------|--------|---------|
| **Mot de passe crypté** | ✅ Fait | Utilisation de `UserPasswordHasherInterface` avec algorithme bcrypt (cost: 12) |
| **Convention de nommage base, table, champs (Anglais, Pas d'espace)** | ✅ Fait | Tables en anglais : `users`, `listings`, `bookings`, `payments`, etc. |
| **MySQL ou PostgreSQL** | ✅ Fait | **PostgreSQL** configuré via Doctrine ORM |

### Entités principales créées :
- `User`, `Listing`, `Booking`, `Payment`, `Review`, `Favorite`
- `Conversation`, `Message`, `Notification`, `Report`
- `Room`, `VisitSlot`, `Contract`, `Subscription`
- 27 migrations Doctrine appliquées

---

## Back

| Critère | Statut | Détails |
|---------|--------|---------|
| **Vérifier la sécurité des routes** | ✅ Fait | Configuration `security.yaml` avec JWT, access_control, rate limiting |
| **Ajouter le Login/Register/Mot de passe oublié** | ✅ Fait | Login ✅, Register ✅, OTP/Vérification téléphone ✅ |
| **Utiliser le modèle MVCS** | ✅ Fait | Architecture Symfony : Controller + Service + Entity/Repository |

### Détails sécurité :
- **JWT** : Lexik JWT Authentication Bundle
- **Rate Limiting** : Protection contre les attaques brute-force
- **Firewalls** : Routes publiques vs protégées configurées
- **Logs de sécurité** : `SecurityLogger` pour tracer les connexions

### Controllers (29 total) :
- `AuthController` : Login, Register, OTP, Profil
- `ListingController` : CRUD annonces
- `PaymentController` : Paiements Wave/Orange Money
- `AdminController`, `ModerationController`, `ReviewController`, etc.

### Services (25 total) :
- `SMSService`, `SecurityLogger`, Services de paiement, etc.

---

## API

| Critère | Statut | Détails |
|---------|--------|---------|
| **Ajouter Swagger** | ✅ Fait | API Platform avec OpenAPI (`/api/docs`) |
| **Utiliser le modèle MVCS** | ✅ Fait | Services métier séparés des contrôleurs |
| **Middleware pour gérer l'authentification** | ✅ Fait | JWT Middleware via Lexik Bundle |

### Endpoints principaux :
```
POST   /api/v1/auth/login          - Connexion
POST   /api/v1/auth/register       - Inscription
GET    /api/v1/auth/me             - Profil utilisateur (protégé)
GET    /api/v1/listings            - Liste des annonces
POST   /api/v1/listings            - Créer une annonce (protégé)
GET    /api/v1/search/intelligent  - Recherche intelligente
POST   /api/v1/payments/*          - Gestion des paiements
GET    /api/v1/conversations       - Messagerie (protégé)
```

---

## Front

| Critère | Statut | Détails |
|---------|--------|---------|
| **React/Angular** | ✅ Fait | **React 18** avec Vite |
| **Utiliser le modèle MVCS** | ✅ Fait | Architecture avec services séparés (`/src/services/api.js`) |
| **Mettre Axios + Intercepteur (JWT et refresh token)** | ⚠️ Partiellement | Utilise `fetch` avec wrapper `fetchWithAuth` (gestion JWT) |

### Structure Frontend :
```
planb-frontend/
├── src/
│   ├── App.jsx              # Composant principal
│   ├── components/          # Composants réutilisables
│   ├── services/
│   │   └── api.js           # Service API centralisé
│   └── assets/
├── public/                   # PWA assets
├── tailwind.config.js       # TailwindCSS
└── vite.config.js           # Configuration Vite
```

### Service API (`api.js`) :
- **Token Management** : `getToken()`, `setToken()`, `removeToken()`
- **Intercepteur JWT** : Gestion automatique du header `Authorization: Bearer`
- **Gestion 401** : Redirection automatique vers login si token expiré
- **Services** : `authService`, `listingService`, `paymentService`, `favoriteService`, `messageService`, etc.

---

## Fonctionnalités Bonus Implémentées

| Fonctionnalité | Statut |
|----------------|--------|
| **PWA (Progressive Web App)** | ✅ Fait |
| **Socket.IO (Chat temps réel)** | ✅ Fait |
| **Paiements Mobile Money (Wave, Orange)** | ✅ Fait |
| **Système de notifications push** | ✅ Fait |
| **Système d'avis et reviews** | ✅ Fait |
| **Recherche intelligente** | ✅ Fait |
| **Système de modération** | ✅ Fait |
| **Carte interactive (Leaflet)** | ✅ Fait |
| **Visite virtuelle** | ✅ Fait |
| **Multi-plateforme (Web + Mobile)** | ✅ Fait |

---

## Points à Améliorer (Recommandations)

1. **Gestion des tâches** : Ajouter GitHub Issues ou Trello pour le suivi
2. **Documentation technique** : Ajouter un MCD/ERD pour la base de données
3. **Mockups** : Lier les maquettes Figma dans le README
4. **Axios** : Migrer de `fetch` vers Axios pour bénéficier des intercepteurs natifs
5. **Refresh Token** : Implémenter un système de refresh token complet
6. **Tests** : Ajouter des tests unitaires et d'intégration
7. **Docker** : Dockerfile présent, à documenter pour le déploiement

---

## Résumé

| Section | Score |
|---------|-------|
| Organisation | 2/5 ⚠️ |
| BDD | 3/3 ✅ |
| Back | 3/3 ✅ |
| API | 3/3 ✅ |
| Front | 2/3 ⚠️ |
| **TOTAL** | **13/17** |

---

*Document généré pour évaluation du projet Plan B*
