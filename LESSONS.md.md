# 🧠 Erkenntnisse aus der Prozessfähigkeitsanalyse

## 📉 convex_volume – das scheinbar wichtigste Merkmal

Obwohl `convex_volume` laut Feature Importance das stärkste Merkmal zur Klassifikation im ML-Modell war, zeigt die Cp/Cpk-Analyse:

- **Cp = 0.48** ❌
- **Cpk = 0.34** ❌

Das bedeutet: Die physikalische Ausprägung des Merkmals `convex_volume` (Lötvolumen) unterliegt einer **hohen Streuung** und ist **nicht gut zentriert**.

---

## 🛠️ Wichtige Klarstellung:

> Die statistische Unfähigkeit betrifft **nicht den AOI-Prozess selbst**, sondern den **vorgelagerten Lötprozess**.

- Der AOI misst nur, was durch Löten entsteht – also Lötmenge, Form, Abstand usw.
- Die Varianz im `convex_volume` ist ein Hinweis auf Prozessprobleme wie:
  - ungleichmäßiger Flussmittelauftrag
  - Dosierschwankungen
  - mechanische Toleranzen im LP-Handling
- Der AOI erkennt aktuell fehlerfrei, aber:
  - **Wenn der Lötprozess instabil ist**, wird die AOI-Klassifikation langfristig anfällig (z. B. für Fehlalarme)

---

## 🎯 Lektion:

> Ein gutes Machine Learning-Modell ersetzt keine Prozessstabilität.  
> Und ein AOI erkennt nur, was da ist – es kann keine Prozessdrift verhindern.

📌 Die Cp/Cpk-Analyse ist ein Werkzeug zur Bewertung der **Produktionsstabilität**, nicht der AI-Leistung.

---

## ✅ Fazit:

Diese Erkenntnis wurde bewusst dokumentiert, um die Abgrenzung zwischen Messsystem (AOI), Analysemodell (ML) und Prozessursache (Lötprozess) klarzustellen.  
Sie zeigt, warum in der Produktion **alle Ebenen gemeinsam** betrachtet werden müssen, um Schlupf, Scheinfehler und Nacharbeit dauerhaft zu vermeiden.