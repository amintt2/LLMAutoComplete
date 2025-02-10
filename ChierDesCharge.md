# Cahier des Charges : Auto-complétion Locale Intelligente (v4)

---

## 1. Objectifs ✨

*   **Complétion en temps réel :** Fonctionne discrètement avec toutes vos applications (sauf celles que vous excluez !).
*   **IA 100% locale :** Modèles de langage (1B ou 3B) rapides et respectueux de votre vie privée (Llama.cpp).
*   **Sécurité renforcée :** Aucune donnée ne quitte votre machine. Conception anti-intrusion.
*   **Multiplateforme :** Windows, macOS, Linux, on est partout !
*   **Ultra-personnalisable :** Adaptez l'outil à vos besoins (suggestions, zones de texte, etc.).

---

## 2. Architecture & Technologies ⚙️

### Approche Générale

*   **Développement natif par plateforme :** Code spécifique à chaque OS pour une intégration optimale.
    *   **macOS :** Input Method Editor (IME) avec Input Method Kit (Swift/Objective-C).
    *   **Windows :** Text Services Framework (TSF) IME (C#/C++).
    *   **Linux :** Module IBus/Fcitx (C/C++/Python).
*   **Architecture commune :**
    *   Service/démon en arrière-plan (langage natif) : Capture de texte, inférence LLM (Llama.cpp), communication inter-processus (IPC).
    *   Interface utilisateur (langage natif ou React avec un pont) : Affichage des suggestions, paramètres.
* **Communication Inter-Processus (IPC):**
    *   Chaque version pourra utiliser une architecture en deux volets : un service de capture et d'inférence (écrit dans un langage performant adapté à l'OS) et une interface utilisateur (native). La communication entre ces modules se fera par des mécanismes d'IPC adaptés (sockets, pipes nommés, ou API spécifiques).

### Cœur du Système (Commun)

*   **Moteur d'inférence :** Intégration optimisée de Llama.cpp (bindings C).
*   **Capture de texte intelligente :**
    *   Techniques avancées : API natives + OCR (Tesseract, etc.) en secours.
    *   Réactivité : Déclenchement uniquement en cas de changement important (méthode à choisir).

### Interface & Orchestration

*   **Logique applicative :** Gestion des événements, appels au moteur d'inférence.
*   **Interface utilisateur :** Native (Swift/Objective-C, C#/C++, framework natif Linux) ou React (avec un pont vers le code natif).

---

## 3. Fonctionnalités Clés 🔑

1.  **Capture de texte :**
    *   Détection intelligente des changements à l'écran.
    *   Priorité aux API natives, OCR en secours.
    *   Gestion des erreurs OCR.

2.  **Traitement LLM :**
    *   Llama.cpp au cœur.
    *   Fine-tuning local (optionnel) :
        *   Données : Vos logs anonymisés (avec votre accord !) ou données open source.
        *   Outils : Hugging Face Transformers, etc.
    *   Gestion des modèles :
        *   Téléchargement facile (méthode à choisir) et sélection (1B, 3B, versions fine-tunées).
        *   Stockage local sécurisé, mises à jour avec vérification d'intégrité.
    *   Optimisation : Vitesse maximale (quantification, batching, etc.).

3.  **Interface Utilisateur :**
    *   Discrète : Suggestions "légèrement grisées" (méthode d'affichage à préciser).
    *   Intuitive : Navigation clavier/souris.
    *   Personnalisable : Paramètres pour tout contrôler.
    *   Design cohérent entre les plateformes, respectant les guidelines de chaque OS.

4.  **Workflow Utilisateur :**
    1.  Vous tapez.
    2.  Le code natif détecte un changement.
    3.  Le texte est capturé.
    4.  Llama.cpp propose des suggestions.
    5.  Le code natif transmet à l'interface.
    6.  Vous choisissez (ou pas) avec Tab.

---

## 4. Qualité, Sécurité & Éthique ✅

*   **Tests rigoureux :** Unitaires, intégration, système, performance (spécifiques à chaque plateforme). Intégration continue (CI) *pour chaque plateforme*.
*   **Gestion des erreurs :** Messages clairs et solutions proposées.
*   **Sécurité sans compromis :** Analyse des risques, permissions limitées, sandboxing, chiffrement (à discuter).
*   **Transparence :** Licence open source, information claire sur les données.

---

## 5. Points à Finaliser 🎯

1.  **Framework d'interface utilisateur :** Natif ou React (avec pont) ?
2.  **Détection de changement :** Préciser la méthode.
3.  **Téléchargement des modèles :** Choisir la méthode (direct, BitTorrent).
4.  **Affichage des suggestions :** Préciser la méthode (superposition, etc.).
5.  **Communication inter-processus (IPC) :** Choix spécifique pour chaque plateforme (sockets, pipes nommés, etc.).
6.  **Gestion du cycle de vie de Llama.cpp :** Comment le gérez-vous (démarrage, arrêt, redémarrage en cas d'erreur)?
7.  **Cohérence multiplateforme :** Comment assurer une expérience utilisateur cohérente malgré les différences techniques ? (Guide de style commun, API de configuration commune, etc.)

---
## Spécifications Techniques par Système d'Exploitation

### macOS

*   **Mécanisme de saisie :** Input Method Editor (IME) basé sur l'Input Method Kit.
*   **Langages :** Swift ou Objective-C.
*   **Interface Utilisateur :** Interface native (overlay) respectant les guidelines Apple.
*   **Tests :** macOS Catalina et versions ultérieures.

### Windows

*   **Mécanisme de saisie :** Text Services Framework (TSF) IME.
*   **Langages :** C# (.NET) ou C++.
*   **Interface Utilisateur :** Overlay léger et modulable, intégré avec les notifications Windows.
*   **Tests :** Windows 10 et Windows 11.

### Linux

*   **Mécanisme de saisie :** Module pour IBus ou Fcitx.
*   **Langages :** C/C++ ou Python.
*   **Interface Utilisateur :** Interface graphique (overlay) s'intégrant avec l'environnement de bureau (GNOME, KDE, etc.).
*   **Tests :** Universalité sur plusieurs distributions (Ubuntu, Fedora, etc.).

---