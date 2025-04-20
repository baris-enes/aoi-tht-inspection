# 🔍 AOI-THT-Inspection – Solder Ball Detection with Machine Learning

Dieses Projekt simuliert einen praxisnahen AOI-Prozess (Automated Optical Inspection) zur Erkennung von Lotkugeln an THT-Lötstellen (Through-Hole Technology) – basierend auf realer Berufserfahrung in der Automobil-Elektronikfertigung.

Ziel ist es, mittels Machine Learning eine robuste Klassifikation kritischer Lötfehler zu ermöglichen. Der Fokus liegt dabei auf der Erfüllung von Qualitätsanforderungen gemäß IPC-A-610 und IATF 16949 sowie auf der Sicherstellung von Auditfähigkeit und Null-Schlupf-Zielsetzungen in sicherheitsrelevanten Serienprozessen.

---

## 🎯 Projektziele

- Automatisierte Erkennung von Lotkugeln >170 µm Durchmesser
- Kombination aus 2D- und 3D-Prüfung zur Schlupfvermeidung
- Training eines ML-Modells zur Fehlerklassifikation (OK / NOK)
- Auditfähige Nachweise (Cp/Cpk, Golden Samples, Driftanalyse)
- Simulation realer Einflussgrößen wie Trägerverunreinigungen, Glanz, Schatten, Prozesskammerleckage

---

## 🛠️ Technologien

- Python 3.x  
- Scikit-Learn – Decision Tree Classifier  
- Pandas & NumPy – Datenverarbeitung  
- Matplotlib – Visualisierung  
- Jupyter Notebook – Interaktive Analyse  
- (Kontext: Keyence XG-X System mit 2D/3D-Funktionalität)

---

## 🔐 Sicherheitsrelevanz

Das AOI-System dient in diesem Projekt als **Firewall** gegen sicherheitskritische Lötfehler – insbesondere bei Komponenten wie DC/DC-Wandlern. Ein Schlupf würde potenziell zu elektrischen oder thermischen Ausfällen im Fahrzeug führen.

Die AOI-Konfiguration wurde auf:
- **Null-Schlupf**
- **False-Positive-Reduktion**
- **Schnelle Prüfzeit (<6s pro PCB)**  
ausgelegt – in Übereinstimmung mit Sicherheits- und Qualitätsvorgaben der IATF 16949.

---

## 📁 Projektstruktur

```bash
aoi-tht-inspection/
│
├── notebooks/
│   ├── 01_generate_data_with_feature_explanation.ipynb
│   ├── 02_train_model.ipynb
│   └── 03_process_cp_ck.ipynb
│
├── data/
│   └── 01_generated_aoi_data_80_20_ratio_rounded.csv
│
├── diagrams/
│   └── Flowchart_THT_Soldering.png
│
├── docs/
│   └── Projekt_AOI_THT_Zusammenfassung.pdf
│
├── LESSONS.md
└── README.md
```

---

## 📬 Kontakt

**📧** [baris-enes@outlook.de](mailto:baris-enes@outlook.de)  
**www.linkedin.com/in/enes-baris-eng**

---

## ⚠️ Hinweis

> Dieses Projekt basiert auf realen Industrieerfahrungen, wurde jedoch vollständig abstrahiert und anonymisiert.  
> Alle dargestellten Daten und Strukturen sind synthetisch erzeugt. Es besteht keine Verbindung zu bestimmten Unternehmen oder Marken.
