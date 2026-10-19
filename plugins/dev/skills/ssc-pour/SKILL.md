---
name: ssc-pour
description: "Ideen-Eingang auf dem Issue tracker eines Repos mit den mattpocock-Skills. Nutze das, wenn Stephan Ideen ausschüttet ('gieß ein', 'notier als Idee', 'Feature-Idee'), eine Runde will ('Runde', 'Pakete schnüren', 'was bauen wir als Nächstes?') oder auf die Prüfliste einer Runde antwortet."
---

# ssc-pour

Zwei Takte: **eingießen** legt je Idee ein Issue an, ohne zu bewerten; die **Runde** schnürt aus den unbewerteten Issues Pakete und übergibt sie an die mattpocock-Skills.

## Voraussetzung

Das Repo hat `/setup-matt-pocock-skills` durchlaufen. Lies vor dem ersten Schreibzugriff `docs/agents/issue-tracker.md` (Befehle, Wayfinding operations) und `docs/agents/domain.md` (wo das Glossar liegt). Fehlt `issue-tracker.md`, sag Stephan, er soll `/setup-matt-pocock-skills` laufen lassen, und schreib nichts.

Was eine Idee ist: ein Issue **ohne Label**. `/triage` zeigt es als „nie triagiert“.

## Eingießen

Je Gedanke, ein Schwall ergibt mehrere:

1. **Mini-Check:** 2–3 Begriffe aus dem Gedanken, Suche in offenen und geschlossenen Issues (GitHub: `gh issue list --state all --search "<begriffe>" --json number,title,state,labels`) und in `.out-of-scope/`. Nur Titel lesen, nicht in die Tiefe. Fertig, wenn feststeht: Treffer oder keiner.
   - **offenes Issue zum selben Gedanken:** Kommentar dort mit dem neuen Aspekt, kein neues Issue
   - **geschlossen als „später“:** wieder öffnen, Kommentar mit dem neuen Aspekt
   - **abgelehnt (`.out-of-scope/` oder `wontfix`):** nichts anlegen, die Ablehnung mit Link melden
2. **Rückfrage:** höchstens eine, und nur, wenn ohne sie unklar bleibt, *was* anders werden soll. Sonst keine.
3. **Issue anlegen,** ohne Label. Titel kurz, mit den Begriffen des Glossars. Body:

   ```markdown
   ## Idee
   <Stephans Worte, ein bis drei Sätze>

   ## Warum
   <Anlass oder Reibung, wie Stephan sie nennt; ohne Nennung bleibt der Abschnitt leer>

   ## Kontext
   <woran gerade gearbeitet wurde> · <JJJJ-MM-TT>
   ```

4. **Antworten,** eine Zeile je Gedanke: `Im Topf: <Titel> (#N)`, `Ergänzt: <Titel> (#N)` oder `Abgelehnt: <Titel> (#N / Datei)`. Liegen danach 15 oder mehr Issues ohne Label offen, hänge an: `Runde fällig (<Anzahl> unbewertet).`

Mehr nicht: einordnen, bewerten und Pakete schnüren macht die Runde.

## Runde

1. **Lesen:** alle offenen Issues ohne Label (`gh issue list --state open --search "no:label"`), dazu jede offene Map (`--label wayfinder:map`: Destination, Not yet specified) und jedes offene Spec-Issue. Fertig, wenn jede Idee gelesen ist.
2. **Pakete bilden:** Ideen, die ein gemeinsames Ziel haben, nicht nur dieselben Wörter. Je Idee genau ein Vorschlag:

   | Vorschlag | Bedingung | Was nach dem OK passiert |
   |---|---|---|
   | **zu Map X** | liegt innerhalb der Destination einer offenen Map | Zeile unter Not yet specified der Map mit Link auf die Idee; Idee schließen mit Kommentar „→ Map X“ |
   | **berührt Spec Y** | ändert, was eine Spec schon festlegt | Kommentar mit Link an die Spec; Idee bleibt offen, nächster Schritt `/triage` |
   | **neues Paket, unklar** | mehrere Ideen, gemeinsames Ziel, Weg noch im Nebel | nichts schreiben; nächster Schritt `/wayfinder` mit den Nummern |
   | **neues Paket, klar** | Ziel und Weg in einer Sitzung greifbar | nichts schreiben; nächster Schritt `/grill-with-docs`, dann `/to-spec` |
   | **einzeln** | passt in kein Paket | nichts schreiben; nächster Schritt `/triage #N` |
   | **Dublette** | zweites Issue zum selben Gedanken | schließen mit `--duplicate-of` |
   | **später** | gültig, aber weit weg | schließen als *not planned*, Kommentar „später: <Grund im Halbsatz>“ |

   Inhalt einer Map oder Spec änderst du nie: an eine Map nur die Zeile unter Not yet specified, an eine Spec nur der Kommentar. Bewertet wird dort im nächsten `/wayfinder` bzw. `/triage`.
3. **Prüfliste zeigen:** nummeriert, je Idee `N. <Titel> (#nr) → <Vorschlag> – <Begründung im Halbsatz>`, Pakete als Gruppe mit Namen. Fertig, wenn jede Idee aus Schritt 1 genau eine Nummer hat.
4. **Antwort umsetzen:** Stephan antwortet wie „1–4 ok, 5 später, 6 einzeln“. Erst jetzt schreibst du, nur die Spalte „Was nach dem OK passiert“. Nummern ohne Antwort bleiben unverändert.
5. **Übergabe:** Liste der nächsten Schritte, die Stephan startet, je Paket bzw. Einzelidee eine Zeile mit dem Befehl, z. B. `/wayfinder` mit `#12 #15 #19`. Die Runde endet mit dieser Liste; `/triage`, `/wayfinder` und `/to-spec` startest du nicht selbst.
