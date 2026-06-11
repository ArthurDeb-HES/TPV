# Topological Plan Validator

**Validation automatique de plans architecturaux par Homologie Persistante et Décomposition Morse-Smale**

Détection robuste des **hallucinations structurelles** (pièces emmurées, espaces déconnectés) générées par les modèles d’IA (diffusion, GAN, etc.).

---

## Objectif

Les modèles génératifs produisent souvent des plans avec des erreurs topologiques invisibles à l’œil nu (pièces sans accès, corridors bouchés…).  
Ce projet implémente une **pipeline scientifique** qui transforme un plan binaire en un graphe compact (Morse-Smale) puis calcule son **homologie persistante H₀** pour détecter automatiquement toute composante déconnectée.

> **β₀ = 1** → Plan **valide**  
> **β₀ > 1** → Hallucination détectée

---

## Fonctionnalités

- Génération de plans de test avec hallucinations contrôlées
- Calcul de la Transformée de Distance Euclidienne (EDT)
- Décomposition Morse-Smale via Watershed + maxima locaux
- Construction d’un graphe topologique pondéré (NetworkX)
- Filtration simpliciale et homologie persistante avec **Gudhi**
- Visualisations détaillées (EDT, bassins, graphe, diagramme de persistance, barcode)
- Rapport final de validation clair

---

## Technologies

- **Python 3.10+**
- `numpy`, `scipy`, `scikit-image`
- `matplotlib` + `networkx`
- `gudhi` (Topological Data Analysis)
- Jupyter Notebook

---

## Installation

```bash
# 1. Cloner le repository
git clone https://github.com/ArthurDeb-HES/TPV.git
cd TPV

# 2. Créer un environnement virtuel (fortement recommandé)
python -m venv TPV
source TPV/bin/activate          

# 3. Installer les dépendances
pip install -r requirements.txt
```

### Contenu de `requirements.txt`

```txt
numpy>=1.24.0
scipy>=1.10.0
matplotlib>=3.7.0
scikit-image>=0.20.0
networkx>=3.0
gudhi>=3.8.0
pillow>=9.0.0
```

> **Note sur Gudhi** :  
> Si l’installation échoue avec pip, essayez via conda :
> ```bash
> conda install -c conda-forge gudhi
> ```

---

## Utilisation

```bash
jupyter notebook topological_plan_validator.ipynb
```

Le notebook contient tout le pipeline en 4 blocs :

1. **Bloc 1** — Génération du plan test avec hallucination
2. **Bloc 2** — Transformée de Distance Euclidienne (EDT)
3. **Bloc 3** — Construction du Graphe Morse-Smale
4. **Bloc 4** — Homologie Persistante & Décision finale

---

## Exemple de résultat

Le plan de test inclut volontairement une **pièce emmurée** (Pièce C).  
Le pipeline détecte correctement **β₀ = 2** → **Plan rejeté** avec identification de l’hallucination.

---

## Structure du projet

```
TPV/
├── topological_plan_validator.ipynb     # Notebook principal
├── requirements.txt
├── README.md
├── outputs/                             # Images générées (optionnel)
│   ├── bloc1_plan.png
│   ├── bloc2_edt.png
│   ├── bloc3b_graph.png
│   └── bloc4_persistence.png
└── ...
```

---

## Approche Scientifique

Évite le coût prohibitif de l’homologie cubique directe (`O(n³)`) en réduisant le problème à un graphe de taille **O(k)** où *k* est le nombre de pièces.

**Complexité finale** : `O(n² log n)` — scalable sur des plans haute résolution.

---

## Améliorations futures

- Détection H₁ (cycles aberrants)
- Comparaison avec plan de référence (Bottleneck distance)
- Pipeline batch pour filtrage massif
- Interface web (Streamlit / Gradio)

---

## Licence

MIT License

---

**Auteur** : Laurène Recegant et Arthur Debauge 
**Date** : Juin 2026
