# LiFAC Go · chaîne de compilation

Ce dépôt **ne contient aucun code applicatif**. Il contient seulement les fichiers
de configuration qui analysent, testent et compilent l'application mobile LiFAC Go
(Flutter), dont le code vit dans un dépôt privé.

Pourquoi séparer : les machines d'intégration sont gratuites pour un dépôt public,
et le code n'a pas à l'être. Le code privé est cloné dans la machine d'exécution,
vérifié ou compilé, puis la machine est détruite.

- `init-platforms.yml` génère les dossiers Android et iOS d'un projet Flutter neuf.
  Il n'accède à rien de privé.
- `check.yml` analyse, teste et compile le code privé, en mode silencieux.

## Ce qui reste privé, et à quelle condition

| Élément | Visible par tous ? | Protection |
|---|---|---|
| Code de l'application | Non | Cloné à l'exécution avec un jeton en lecture seule, jamais commité ici |
| Clés et jetons | Non | Secrets GitHub, masqués dans les journaux |
| Journaux d'exécution | **Oui** | Mode silencieux : seuls l'emplacement et la règle d'une erreur sortent |
| Artefacts (APK) | **Oui** | Produits seulement sur demande explicite, conservés 3 jours |
| Ces workflows | **Oui** | Qui peut les modifier peut lire le code privé : branche protégée |

Un APK peut être décompilé : un APK publié en artefact révèle une partie du code.

## Réglages attendus

- Variable `MOBILE_REPO` : dépôt privé du code, par exemple `nahim-salami/lifac-go-app`.
- Variable `MOBILE_DIR` (facultative) : dossier du projet Flutter dans ce dépôt (`.` par défaut).
- Secret `MOBILE_REPO_TOKEN` : jeton à grain fin, **lecture seule** (Contents: Read),
  limité au seul dépôt privé.

LiFAC, Light For All Center, Abomey-Calavi, Bénin. Tous droits réservés.
