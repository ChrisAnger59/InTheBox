# InTheBox

Web app de gestion du contenu de boîtes de rangement physiques via QR codes.

On crée une boîte, on y liste ses items, on génère un QR code qu'on imprime et
qu'on colle sur la boîte. En scannant le QR code, on accède directement à la
liste du contenu.

> Projet développé dans un but d'apprentissage de Symfony (premier projet sur ce
> framework). Voir [`CLAUDE.md`](CLAUDE.md) pour le contexte pédagogique.

---

## Fonctionnalités

### MVP (en cours)

- Créer / modifier / supprimer une **boîte** (nom, description, code unique)
- Ajouter / modifier / supprimer des **items** dans une boîte (nom, quantité, description)
- Générer un **QR code** par boîte, encodant une URL `/box/{code_unique}`
- Page de **consultation publique** d'une boîte (accès via scan)
- Mono-utilisateur (pas d'authentification pour l'instant)

### Évolutions envisagées (hors MVP)

- Recherche
- Multi-utilisateurs
- Catégories / tags sur les items
- Dashboard de gestion des boîtes

---

## Stack technique

| Élément            | Choix                          |
| ------------------ | ------------------------------ |
| Langage            | PHP 8.2+                       |
| Framework          | Symfony 7.4 (LTS)             |
| Base de données    | MySQL / MariaDB               |
| ORM                | Doctrine *(à venir)*          |
| Templates          | Twig *(à venir)*             |
| QR code            | `endroid/qr-code` *(à venir)* |
| Environnement local | XAMPP                         |

---

## Prérequis

- PHP >= 8.2 avec les extensions `ctype`, `iconv`, `intl`, `mbstring`, `pdo_mysql`
- [Composer](https://getcomposer.org/) 2.x
- MySQL / MariaDB (fourni par XAMPP)
- [Symfony CLI](https://symfony.com/download) *(optionnel, pour le serveur de dev)*

---

## Installation

```bash
git clone <url-du-dépôt> InTheBox
cd InTheBox
composer install
```

Le fichier `.env` est versionné et fournit les valeurs par défaut : **ne pas le
modifier**. Pour surcharger une variable sur sa machine, créer un fichier
`.env.local` (non versionné) et n'y mettre **que les lignes à surcharger**, par
exemple la connexion base de données lorsque Doctrine sera en place :

```dotenv
# .env.local
DATABASE_URL="mysql://root:@127.0.0.1:3306/inthebox?serverVersion=10.4.32-MariaDB&charset=utf8mb4"
```

> ⚠️ Ne jamais mettre d'identifiants réels dans `.env` (il est commité). Les
> valeurs sensibles vont dans `.env.local`, ou dans de vraies variables
> d'environnement système en production.

---

## Lancer le serveur de développement

Avec le Symfony CLI (recommandé) :

```bash
symfony serve
```

Sans le Symfony CLI, avec le serveur PHP intégré :

```bash
php -S 127.0.0.1:8000 -t public/
```

L'application est alors disponible sur <https://127.0.0.1:8000> (ou `http://`
avec le serveur PHP intégré).

---

## Structure du projet

```
InTheBox/
├── bin/            Exécutables (console Symfony)
├── config/         Configuration (routes, packages, services)
├── public/         Racine web exposée — point d'entrée public/index.php
├── src/            Code applicatif (namespace App\)
│   ├── Controller/
│   └── Kernel.php
├── var/            Cache et logs (non versionné)
└── vendor/         Dépendances Composer (non versionné)
```

---

## Avancement

- [x] Squelette Symfony 7.4 installé
- [ ] Routing + premier contrôleur
- [ ] Twig
- [ ] Entités `Box` / `Item` + Doctrine
- [ ] Repositories
- [ ] Formulaires + validation
- [ ] Génération des QR codes
- [ ] Page publique de consultation

---

## Licence

Propriétaire — usage personnel / pédagogique.
