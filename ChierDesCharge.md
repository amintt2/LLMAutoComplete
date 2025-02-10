# Cahier des Charges : Auto-complétion Locale Intelligente (v3)

---

## 1. Objectifs ✨

*   **Complétion en temps réel :** Fonctionne discrètement avec toutes vos applications (sauf celles que vous excluez !).
*   **IA 100% locale :** Modèles de langage (1B ou 3B) rapides et respectueux de votre vie privée (Llama.cpp).
*   **Sécurité renforcée :** Aucune donnée ne quitte votre machine. Conception anti-intrusion.
*   **Multiplateforme :** Windows, macOS, Linux, on est partout !
*   **Ultra-personnalisable :** Adaptez l'outil à vos besoins (suggestions, zones de texte, etc.).

---

## 2. Architecture & Technologies ⚙️

### Cœur du Système (Rust) : Puissance et Fiabilité

*   **Moteur d'inférence :** Intégration optimisée de Llama.cpp (bindings C, `pyo3` pour Python).
*   **Capture de texte intelligente :**
    *   Fonctionne partout : Couche d'abstraction multiplateforme.
    *   Techniques avancées : API natives (Windows, macOS, Linux) + OCR (Tesseract, etc.) en secours.
    *   Réactivité : Déclenchement uniquement en cas de changement important (méthode à choisir).
*   **Communication fluide :** Service/démon Rust avec API locale (HTTP/WebSocket, framework à choisir).

### Interface & Orchestration (Python) : Flexibilité et Simplicité

*   **Logique applicative :** Gestion des événements, appels à Rust (`pyo3`).
*   **Interface utilisateur :** React (avec Electron pour une version bureau, si besoin).
*   **Lien avec Rust :** Requêtes à l'API locale du service Rust.

---

## 3. Fonctionnalités Clés 🔑

1.  **Capture de texte :**
    *   Détection intelligente des changements à l'écran.
    *   Priorité aux API natives, OCR en secours.
    *   Gestion des erreurs OCR.

2.  **Traitement LLM (Rust) :**
    *   Llama.cpp au cœur.
    *   Fine-tuning local (optionnel) :
        *   Données : Vos logs anonymisés (avec votre accord !) ou données open source.
        *   Outils : Hugging Face Transformers, etc.
    *   Gestion des modèles :
        *   Téléchargement facile (méthode à choisir) et sélection (1B, 3B, versions fine-tunées).
        *   Stockage local sécurisé, mises à jour avec vérification d'intégrité.
    *   Optimisation : Vitesse maximale (quantification, batching, etc.).

3.  **Interface Utilisateur (React + Python) :**
    *   Discrète : Suggestions "légèrement grisées" (méthode d'affichage à préciser).
    *   Intuitive : Navigation clavier/souris.
    *   Personnalisable : Paramètres pour tout contrôler.
    *   Design épuré.

4.  **Workflow Utilisateur :**
    1.  Vous tapez.
    2.  Rust détecte un changement.
    3.  Le texte est capturé.
    4.  Llama.cpp propose des suggestions.
    5.  Python transmet à React.
    6.  Vous choisissez (ou pas) avec Tab.

---

## 4. Qualité, Sécurité & Éthique ✅

*   **Tests rigoureux :** Unitaires, intégration, système, performance, intégration continue.
*   **Gestion des erreurs :** Messages clairs et solutions proposées.
*   **Sécurité sans compromis :** Analyse des risques, permissions limitées, sandboxing, chiffrement (à discuter).
*   **Transparence :** Licence open source, information claire sur les données.

---

## 5. Points à Finaliser 🎯

1.  **Rust/Python :** Confirmer `pyo3`.
2.  **API Rust :** Choisir le framework (Actix-web, Rocket, etc.).
3.  **Détection de changement :** Préciser la méthode.
4.  **Téléchargement des modèles :** Choisir la méthode (direct, BitTorrent).
5.  **Affichage des suggestions :** Préciser la méthode (superposition, etc.).
6.  **Gestion du cycle de vie de Llama.cpp**

---