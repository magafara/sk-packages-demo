# 🛠 TP – Maintenir des applications et des packages partagées

# 1️⃣ Prise en main

Pour ce TP, nous allons préparer les éléments nécessaires : nous créerons un nouveau projet GitHub à partir du starter kit, puis nous l’explorerons afin de comprendre son fonctionnement ainsi que les dépendances liées aux packages de configuration du toolkit

### 📦 Étape 1 – Cloner le starter kit

Le starter kit est disponible ici : https://github.com/Zenika/sk-packages-demo

#### Instructions

1. Forker le repository dans votre compte GitHub
2. Cloner votre fork en local
3. Installer les dépendances
4. Lancer le projet
5. Vérifier que tout fonctionne correctement
6. Explorer le projet pour comprendre son architecture et fonctionnement, notamment le `package.json`

### 🔎 Étape 2 – Comprendre le repository tools

Les packages du toolkit sont définis ici : https://github.com/Zenika/sk-packages-tools

#### Instructions

- Parcourir le repository
- Comprendre comment il est structuré
- Identifier comment il est utilisé côté starter kit :
    - Où est-il déclaré ?
    - Comment est-il consommé ?
    - Quelle version est utilisée ?

---

# 2️⃣ Installation de Renovate

Maintenant que nous disposons d’une application fonctionnelle basée sur le starter kit, nous allons y installer Renovate pour automatiser la mise à jour de nos dépendances.

### 📌 Étape 1 – Installer Renovate

1. Ajouter l’application renovate à votre GitHub : https://github.com/apps/renovate/
   - Autoriser Renovate à accéder à votre projet fraichement créé
2. Vous allez être rediriger vers le dashboard web de renovate (https://developer.mend.io/)
   - Installer l’option `Renovate Only` sur le projet
   - Sélectionner le mode `Scan and Alert`

Renovate devrait maintenant avoir accès à votre projet ! Depuis le dashboard, vous pouvez vérifier qu’il a probablement commencé à analyser vos fichiers.

### ✅ Étape 2 – Initialiser Renovate

Afin que renovate soit officiellement opérationnel, vous allez devoir l'initialiser :

* Une PR de onboarding devrait apparaître sur votre projet
   * Vérifier son contenu et merger la

Cette PR va initialiser la configuration par défaut de Renovate, nous verrons par la suite comment la personnaliser.

Après le merge, Renovate peut commencer à créer des PR automatiquement.

> 🚨 Il se peut que la PR n'apparaisse pas et que votre renovate soit en "silent mode".
>
> 👉 Sur le dashboard, aller dans `Settings` ➡️ `Dependencies` et désactiver "silent mode".
>
> ✅ Le reste des options devrait rester activés. Sauvegarder et vérifier que renovate c'est bien relancé sur le dashboard.

### 📊 Observer le dashboard

Vous pouvez consulter le dashboard :
- https://developer.mend.io/
- Ou l’issue GitHub créée automatiquement

👀 Observer les dépendances détectées et les PR créées afin de comprendre le comportement par défaut de Renovate.

---

# 3️⃣ Configuration de Renovate

### 📚 Documentation des options montrées sur les slides

schedule : https://docs.renovatebot.com/configuration-options/#schedule

packageRules : https://docs.renovatebot.com/configuration-options/#packagerules

groupName : https://docs.renovatebot.com/configuration-options/#groupname

prConcurrentLimit : https://docs.renovatebot.com/configuration-options/#prconcurrentlimit

osvVulnerabilityAlerts : https://docs.renovatebot.com/configuration-options/#osvvulnerabilityalerts

vulnerabilityAlerts : https://docs.renovatebot.com/configuration-options/#vulnerabilityalerts

---

### 🛠 Exercice – Construire une configuration utile

A l'aide de la [documentation](https://docs.renovatebot.com/configuration-options), mettre à jour le fichier `renovate.json` afin de :

- [ ] Etendre la configuration de base proposée par le toolkit
  - `extends` 
  - La configuration se trouve [ici](https://github.com/Zenika/sk-packages-tools/blob/main/packages/renovate/default.json) : `github>Zenika/sk-packages-tools//packages/renovate/default`  
-[ ] Détecter les dépendances avec une faille de sécurité
  - `osvVulnerabilityAlerts, vulnerabilityAlerts`
-[ ] Limiter les PR concurrentes à 5
  - `prConcurrentLimit`
-[ ] Ajouter un préfixe aux branches Renovate : `renovate-` pour facilement les différencier des autres branches
  - `branchPrefix`
-[ ] Ajouter un préfixe de commit pour les PR
  - `packageRules, commitMessagePrefix`
-[ ] Attendre au minium 3 jours avant d'autoriser une mise à jour de dépendance
  - `packageRules, minimumReleaseAge, matchDatasources`
-[ ] Créer un groupe pour autoriser l'automerge uniquement sur les patchs
  - `packageRules, matchUpdateTypes, automerge`

💡 N'hésitez pas à ajouter d'autres règles que vous pensez intéressante !

### 🎯 Objectif final
- Une configuration claire et maîtrisée
- Un comportement cohérent
- Un nombre de PR raisonnable
- Un auto-merge sécurisé

### 🧩 Aide

Une solution est disponible sur une branche du starter kit.
Comparer votre configuration avec la solution après avoir tenté l’exercice.