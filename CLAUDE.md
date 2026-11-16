# CLAUDE.md — module Dolibarr `factor`

## Description

Module Dolibarr (éditeur **ATM Consulting**) de **gestion de l'affacturage** : sélection de
factures clients, génération du fichier d'export vers le factor (ex. Natixis) et fusion des
PDF de factures associées. Se branche sur la fiche facture et la génération PDF.

Hooks (`module_parts['hooks']`) : `invoicecard`, `formfile`, `pdfgeneration`.
Trigger : `core/triggers/interface_99_modFactor_Factortrigger.class.php`.

## Stack & compatibilité

- PHP ≥ 7.0 (`phpmin`), Dolibarr ≥ 16.0 (`need_dolibarr_version`).
- Configuration via `config.php` (modèle : `config.default.php`).
- `backport/v19/core/class/commonhookactions.class.php` : classe cœur vendorisée pour les
  Dolibarr anciens (rétro-compat, sélectionnée selon la version cœur).

## Structure

| Chemin | Rôle |
|---|---|
| `core/modules/modFactor.class.php` | Descriptor (`numero=104905`, `version`, `module_parts`: triggers+hooks) |
| `factor.php` | Page principale du module (sélection factures / export) |
| `class/factor.class.php` | Logique métier de l'affacturage / export |
| `class/actions_factor.class.php` | Classe de hook (`invoicecard`, `formfile`, `pdfgeneration`) |
| `class/techatm.class.php` | Helper ATM (`TechATM`) — URL de dernière version |
| `core/triggers/interface_99_modFactor_Factortrigger.class.php` | Trigger du module |
| `lib/factor.lib.php` | Utilitaires (export, code compta client) + onglets admin |
| `admin/factor_setup.php` / `_about.php` | Configuration et « À propos » |
| `script/create-maj-base.php` | Script de création / mise à jour de base |
| `config.php`, `config.default.php`, `doc/`, `langs/`, `ChangeLog.md` | Config, docs, traductions, journal |

## Build / test

- Pas de suite de tests automatisée embarquée.
- Vérif syntaxe : `find . -name '*.php' -not -path './vendor/*' -exec php -l {} \;` (gate = 0 erreur).
- Gates qualité ATM au commit (ordre fixe) : `lint → tests → claudemd → docs → techatm → local`
  via `~/.config/team-ai/githooks/commit-msg` (dry-run : `TAC_CHECK_ONLY=1 …`).

## Conventions

- **Code, commentaires, logs et identifiants en anglais.** Les chaînes utilisateur passent par `langs/`.
- Compta : utiliser `Societe::code_compta_client` (avec fallback `code_compta`) — `code_compta`
  n'est plus peuplé par `fetch()` depuis Dolibarr récent (corrigé en 1.6.1).
- SQL en requêtes préparées, échappement à l'affichage, comparaisons strictes (`===`).
- **Releases de compatibilité** : une passe de compat majeure produit *toujours* une release,
  même sans changement de code. Bump **PATCH** (Z+1) du `$this->version` dans le descriptor +
  une ligne en tête du bloc `## Release X.Y` du `ChangeLog.md`, au format existant :
  `- FIX : COMPAT V<NN> - *DD/MM/YYYY* - X.Y.Z`.
- **Branches / PR** : ligne de version `X.Y` (la plus récente = base de travail), branche de fix
  `FIX/COMPAT/V<NN>`, PR vers la ligne de version **et** PR `PULLUP:` vers `main`
  (les deux issues de la même branche de fix).
- Repo : `git@github.com:ATM-Consulting/dolibarr_module_factor.git`, branche par défaut `main`.
