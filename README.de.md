# PCOS-Klassifikation mit Machine Learning

[English](README.md) | [**Deutsch**](README.de.md)

## Projektübersicht

Dieses Projekt untersucht die Klassifikation des polyzystischen Ovarsyndroms (PCOS) anhand klinischer und lebensstilbezogener Merkmale. Verschiedene überwachte Lernverfahren werden verglichen, um Beobachtungen mit der Zielvariable `PCOS (Y/N)` zu klassifizieren.

**Ziel:** Reproduzierbare binäre Klassifikationsmodelle entwickeln und vergleichen. Besonderes Augenmerk liegt auf Recall, Precision, F1-Score und ROC-AUC für die positive PCOS-Klasse. Die Analyse ist explorativ und nicht für medizinische Entscheidungen geeignet.



## Methodik

1. **Datenbereinigung:** Spaltennamen vereinheitlichen, fehlende Werte und Duplikate prüfen sowie Identifikatoren und ausgewählte Merkmale entfernen.
2. **Feature Engineering:** Links- und rechtsseitige Follikelmerkmale zu Maximum-Merkmalen zusammenfassen.
3. **Explorative Analyse:** Verteilungen, Zusammenhänge und mögliche Ausreißer mit Statistik und Visualisierungen untersuchen.
4. **Datenaufteilung:** Stratifizierter 80/20-Split und fünffache stratifizierte Kreuzvalidierung ausschließlich auf den Trainingsdaten.
5. **Modelle:** Logistische Regression, Decision Tree, Random Forest, XGBoost und eine Dummy-Baseline vergleichen.
6. **Optimierung:** Hyperparameter mit GridSearchCV bzw. RandomizedSearchCV anhand der ROC-AUC abstimmen. Klassenungleichgewicht über Klassengewichte bzw. `scale_pos_weight` berücksichtigen.
7. **Evaluation:** ROC-AUC, PR-AUC, Precision, Recall, Spezifität, F1 und weitere Kennzahlen auf dem zurückgehaltenen Testsatz auswerten.



## Ergebnisse

Die Kennzahlen stammen aus **gespeicherten Notebook-Ausgaben** und wurden nicht unabhängig neu berechnet. Modellauswahl und Optimierung erfolgten anhand der Trainings-Kreuzvalidierung. Die Tabelle zeigt Testkennzahlen beim Schwellenwert 0,5.

| Modell | Test ROC-AUC | Precision (PCOS) | Recall (PCOS) | F1-Score |
|---|---:|---:|---:|---:|
| Random Forest | **0,9547** | **0,9667** | 0,8056 | **0,8788** |
| XGBoost | 0,9486 | 0,8857 | **0,8611** | 0,8732 |
| Logistische Regression | 0,9326 | 0,7750 | **0,8611** | 0,8158 |
| Decision Tree | 0,9422 | 0,7949 | **0,8611** | 0,8267 |

**Ausgewähltes Modell:** Random Forest, da es die höchste Trainings-CV-ROC-AUC von 0,9595 erzielte. Die Test-ROC-AUC betrug 0,9547. XGBoost erreichte dagegen einen höheren Recall (0,8611 statt 0,8056). Dies verdeutlicht den Zielkonflikt zwischen Recall und Precision.



## Interpretation und Einschränkungen

- Der Datensatz ist relativ klein; eine Übertragung der Ergebnisse auf andere Populationen ist nicht gesichert
- Die Kennzahlen basieren auf einer Testaufteilung; eine externe Validierung fehlt
- Feature Importance zeigt mögliche prädiktive Zusammenhänge, **keine Kausalität**
- Im Gesundheitskontext sind übersehene positive Fälle relevant. Ein anderer Schwellenwert könnte Recall und Precision verändern, wurde aber nicht für einen klinischen Einsatz validiert
- Das Projekt dient **ausschließlich Lern- und Demonstrationszwecken**, nicht der Diagnostik

