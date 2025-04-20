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

## 🧪 2D-/3D-Prüfung mit Keyence – Technologischer Hintergrund

Das Projekt orientiert sich an der Keyence XG-X Plattform – einem industrietauglichen AOI-System für hochpräzise Inline-Prüfungen. Beide Prüfmethoden (2D und 3D) sind redundant aufgebaut und technisch exakt aufeinander abgestimmt:

| Prüfebene | Beschreibung |


| **2D-Prüfung** | Farbbildauswertung über eine 9,44 Megapixel RGB-CMOS-Kamera. Mit drei Spektral-LEDs (Rot, Grün, Blau) und intelligenten Filteralgorithmen werden optische Merkmale wie **Schatten, Glanz, Flussmittelreste, Schlieren, Fräserstaub und Trägerabdrücke** erkannt. Die Beleuchtung eliminiert Reflexionen, und OCR-Algorithmen ermöglichen sogar das Auslesen kleinster Beschriftungen. |

| **3D-Prüfung** | Erfassung realer Geometrie durch strukturierte Lichtprojektion (vier RGB-Projektoren in 90°-Winkeln) und telezentrische Optik. Ermittelt werden u.a. **Volumen, Höhe, Querschnittsfläche, Rundheit, Ferret-Abstände**. Mit **3D Blob Analyse** und **Subtraktionsverfahren** können auch kleinste Lotkugeln sicher detektiert werden, selbst bei stark glänzenden Oberflächen. |

**Hinweis zur Genauigkeit:**  
Ein zentrales Problem strukturierter Lichtprojektion ist die Entstehung sogenannter **Moiré-Effekte** – diese entstehen, wenn das projizierte Streifenmuster mit der Pixelstruktur des Kamerasensors interferiert. Besonders bei nicht-telezentrischen Objektiven, bei denen die Lichtstrahlen unter unterschiedlichen Winkeln auf das Objekt und den Sensor treffen, kommt es zu **Verzerrungen** in der Streifenaufnahme. Das bedeutet: Der Sensor nimmt das Streifenmuster nicht geometrisch korrekt auf, sondern winkelabhängig – was die 3D-Auswertung verfälscht.  

**Lösung:**  
Durch den Einsatz **telezentrischer Optik** bleiben die Lichtstrahlen parallel, sodass das projizierte Muster unabhängig von Objektposition und -höhe **maßstabsgetreu und verzerrungsfrei** auf den Sensor trifft. Dadurch wird die Entstehung unregelmäßiger Moiré-Muster stark reduziert und die **präzise Höhenmessung auch bei schwierigen Oberflächen** gewährleistet. |

Diese duale Struktur ermöglicht eine präzise, sichere und **auditfähige Lötstellenprüfung**.

---

## 🔐 Sicherheitsrelevanz

Das AOI-System dient in diesem Projekt als **Firewall** gegen sicherheitskritische Lötfehler – insbesondere bei Komponenten wie DC/DC-Wandlern. Ein Schlupf würde potenziell zu elektrischen oder thermischen Ausfällen im Fahrzeug führen.

Die AOI-Konfiguration wurde auf:
- **Null-Schlupf**
- **False-Positive-Reduktion**
- **Schnelle Prüfzeit (<1s pro PCB)**  
ausgelegt – in Übereinstimmung mit Sicherheits- und Qualitätsvorgaben der IATF 16949.

---

## 📅 Langzeitdrift & Requalifikation

Die Prüfung der langfristigen Stabilität wurde über sogenannte **Golden Samples** sichergestellt, die regelmäßig vom AOI gescannt wurden.

Wichtige Requalifikationspunkte:
- Oxidation von Golden Samples → beeinflusst Erkennungsrate
- Drift durch Alterung der Beleuchtungseinheit / Kamera oder durch Crashfahrten der Produktionszelle 
- Verunreinigungen durch Werkstückträger (z. B. Flussmittelrückstände, mechanische Abdrücke)
- Prozesskammerleckagen (Stickstoffkammer) als Einflussfaktor

Alle Beobachtungen wurden über **Cp- und Cpk-Werte** dokumentiert und bewertet.

---

## 🔄 AOI-Logik – Entscheidungsstrategie

```plaintext
AOI Inspection
↓
2D Detection
├─ Yes → NOK → Rejection conveyor
│              ↘︎ Manual inspection → False? → back to AOI
│                                    True? → QE decides: scrap / rework / release
└─ No
    ↓
  3D Detection
  ├─ Yes → NOK → Rejection conveyor
  │              ↘︎ Manual inspection → False? → back to AOI
  │                                    True? → QE decides: scrap / rework / release
  └─ No → OK
```

---

## 🧠 Machine Learning

Ein einfacher, aber robuster **Decision Tree Classifier** wird auf synthetische Merkmale trainiert:

- Konvexvolumen (mm³)
- Max. Höhe (Z-Achse)
- Fläche (mm²)
- Rundheit (0–1)
- Abstand zum Referenzpad (simuliert)

Ziel: **Binäre Klassifikation (OK / Lotkugel vorhanden)**

Später können alternative Modelle wie Random Forest, SVM oder sogar ein CNN ergänzt werden.

---

## 📁 Projektstruktur

```bash
aoi-tht-inspection/
│
├── notebooks/
│   ├── 01_generate_data.ipynb        # Simulation von Lötstellenmerkmalen
│   ├── 02_train_model.ipynb          # Modelltraining & Evaluation
│   └── 03_process_cp_cpk.ipynb       # Statistische Prozessfähigkeit
│
├── data/
│   └── golden_samples/               # Requalifikationsmuster
│
├── diagrams/
│   └── aoi_flowchart.png             # Entscheidungslogik (2D/3D)
│
├── src/
│   └── logic.py                      # AOI-Prozess inkl. QE-Logik
│
└── README.md
```

---

## 📬 Kontakt

**📧** [baris-enes@outlook.de](mailto:baris-enes@outlook.de)  
*(Optional: LinkedIn-Profil einfügen)*

---

## ⚠️ Hinweis

> Dieses Projekt basiert auf realen Industrieerfahrungen, wurde jedoch vollständig abstrahiert und anonymisiert.  
> Alle dargestellten Daten und Strukturen sind synthetisch erzeugt. Es besteht keine Verbindung zu bestimmten Unternehmen oder Marken.

> 💡 **SAP Fiori Kontext:**  
> Im realen Projekt wurde SAP Fiori zur **Prozessfreigabe** genutzt – u. a. zur Dokumentation von:  
> • Undichtigkeiten in der Stickstoff-Prozesskammer  
> • Verunreinigungen und Zustand der Werkstückträger  
> Eine direkte Kopplung an das AOI-System bestand nicht.
