Du kommst an der Stelle am besten weiter, wenn du den Fokus im Kapitel von “kryptografische Maßnahmen fehlen” auf “wo wird Security stattdessen umgesetzt” verschiebst.

Dann kannst du sauber begründen, warum in nicht netzwerkfähigen Feldgeräten der Stand der Technik praktisch oft aus Kompensation besteht.

1. Security wird in der Umgebung umgesetzt (Zone, physischer Schutz, Prozesse)
2. Am Gerät gibt es Basisschutzfunktionen, aber kaum Ende zu Ende Kryptografie auf dem Feldbus
3. Die Lücke ist genau der Einstieg in deine Thesis (gerätebasierte Identität, Authentifizierung, sicherer Verbindungsaufbau trotz unsicherem Kanal)

Was du aus deinen Punkten streichen oder stark kürzen kannst

1. CR 1.3, 1.4, 1.10 bis 1.12 (Nutzerkontenverwaltung, Kennungen, Hinweise, UI Feedback)
   Für typische 2 Draht Geräte ohne Benutzerverwaltung sind das Randthemen. Du kannst das als einen Satz zusammenfassen: keine Nutzerkonten, Logging ohne Benutzerbezug, dadurch nur eingeschränkt nachvollziehbar.

2. CR 3.5 bis 3.7 (Eingabevalidierung, definierte Ausgangszustände, Fehlerbehandlung)
   Das sind eher generische Softwarequalitätsthemen. Wenn du sie erwähnst, dann nur als “robustness”, nicht als kryptografische Security.

3. Verfügbarkeit der Ressourcen
   Nur reinnehmen, wenn du später DoS oder Energie Budget wirklich als Angriffsvektor nutzt. Sonst lenkt es ab.

Was du behalten solltest, weil es deinen roten Faden trägt

1. Der klare Satz aus der VEGAPULS 6X Guideline, dass HART keinen ausreichenden Schutz gegen Manipulation und Spionage bietet und daher nur unter SL1 Bedingungen bzw. mit physischem Schutz vertretbar ist ([VEGA][1])
   Das ist die perfekte Brücke von “Protokoll kann es nicht” zu “Umgebung muss es kompensieren”.

2. Einordnung Security Level: SL2 ist in vielen Dokumenten der Punkt, ab dem gezielte, vorsätzliche Angriffe adressiert werden (und damit typischerweise stärkere Authentifizierung und Secure Channel Anforderungen relevant werden) ([support.industry.siemens.com][2])
   Du musst nicht behaupten “steht exakt so in IEC 62443”, sondern kannst sauber formulieren “in der Praxis gilt SL2 häufig als Mindestniveau gegen vorsätzlichen Missbrauch”.

3. Die “Geräteschutzfunktionen” aus der Guideline: Passwortschutz, Firmware Integritätschecks, Logging, Ressourcenmanagement, Backup ([fcc.report][3])
   Wichtig dabei: das sind überwiegend lokale Schutzfunktionen, kein kryptografisch geschützter Kommunikationskanal.

4. Dein SL1 vs. “fehlende” Punkte Block (CR 1.2, 1.8, 3.8)
   Das sind genau die Anforderungen, die du später mit IDevID und einem Key Exchange adressierst. Inhaltlich passt das sehr gut, wenn du es als “Gap” formulierst.

Vorschlag für den Abschnittsaufbau direkt nach deinem letzten Absatz

Du hast aktuell mit “Technische Einschränkungen” logisch abgeschlossen. Danach würde ich genau diese drei Absätze setzen:

1. Einordnung nach IEC 62443: Security Level und Kompensation
2. Praxisbeispiel VEGAPULS 6X: was ist umgesetzt, was wird ausgelagert
3. Verbleibende Lücken: keine Ende zu Ende Kryptografie, keine Geräteauthentifizierung, keine Sitzungen, Motivation für diese Arbeit

Textbaustein als LaTeX, passend zu deinem bisherigen Stil

```latex
% Praxisumsetzung und Einordnung nach IEC 62443
\paragraph{Einordnung nach IEC 62443 und kompensierende Maßnahmen}
In der IEC-62443-Familie werden Sicherheitsanforderungen für Komponenten im Kontext eines übergreifenden Zonen- und Leitungsmodells betrachtet.
In der industriellen Praxis wird dabei häufig davon ausgegangen, dass Schutzmaßnahmen für einfache Komponenten nicht ausschließlich durch das Feldgerät selbst, sondern durch kompensierende Maßnahmen in der Umgebung erreicht werden.
Insbesondere Security Level 2 wird in vielen Industriepublikationen als das niedrigste Niveau eingeordnet, ab dem Schutz gegen vorsätzlichen Missbrauch adressiert wird.
Dies verdeutlicht die Lücke zwischen klassischen Feldgeräteprotokollen ohne integrierte Security-Funktionen und den Anforderungen, die bei gezielten Angriffen typischerweise relevant werden.

\paragraph{Praxisbeispiel: Security-Umsetzung bei einem nicht netzwerkfähigen Feldgerät}
Am Beispiel eines 2-Draht-Feldgeräts (VEGAPULS 6X mit 4~\dots~20\,mA/HART) zeigt sich, dass Sicherheitsfunktionen in der Praxis stark auf lokale Schutzmechanismen und organisatorische Maßnahmen verteilt werden.
Die zugehörige Security Guideline weist explizit darauf hin, dass das standardisierte HART-Protokoll keinen ausreichenden Schutz gegen Datenmanipulation und Spionage bietet und deshalb nur in einer Umgebung mit Schutzniveau entsprechend SL1 bzw. bei sichergestelltem physischem Zugriffsschutz auf die Signalleitungen betrieben werden soll.
Für Schnittstellen und den Gerätezugang werden daher Maßnahmen wie Zugriffsschutz per Passwort, Deaktivierung ungenutzter Kommunikationskanäle sowie physische Sicherungen (z.\,B. Verplombung) gefordert.
Geräteseitig werden zudem Funktionen wie Firmware-Integritätsprüfungen, Ereignisspeicher (Logging) und Ressourcenmanagement als Sicherheitsfunktionen genannt.
Diese Maßnahmen erhöhen die Härtung des Geräts, ersetzen jedoch keinen kryptografisch geschützten Kommunikationskanal auf dem Feldbus.

\paragraph{Verbleibende Lücken auf Protokollebene}
Aus Sicht der Schutzziele Vertraulichkeit, Integrität und Authentizität verbleibt bei nicht netzwerkfähigen Feldgeräten insbesondere eine Lücke in der Ende-zu-Ende-Absicherung der Kommunikation.
Während Integrität im Feldbuskontext häufig nur über einfache Prüfsummen oder CRC-Mechanismen adressiert wird, existieren typischerweise keine Verfahren zur kryptografischen Authentifizierung von Geräten, keine aushandelbaren Sitzungsschlüssel und keine Verschlüsselung der Nutzdaten auf der Leitung.
Damit kann ein Angreifer mit physischem Zugriff auf die Signalleitung Daten mitlesen oder manipulieren, ohne durch das Protokoll selbst zuverlässig detektiert oder ausgeschlossen zu werden.
Genau an dieser Stelle setzt die vorliegende Arbeit an, indem eine gerätebasierte Identität über Zertifikate und ein sicherer Verbindungsaufbau auch für nicht IP-basierte Kommunikationskanäle konzipiert und umgesetzt wird.
```

Wie du deine IEC 62443 Mapping Tabellen schlanker und “thesis-tauglich” bekommst

Statt alle CRs aufzulisten, mach eine reduzierte Tabelle mit genau den Zeilen, die deinen Gap zeigen.

1. Zeigen was heute typisch umgesetzt wird (Passwortschutz, Firmware Integrität, Logging)
2. Zeigen was für Secure Channel fehlt (Geräteauthentifizierung, PKI, Sitzungsintegrität)
3. Eine Spalte “Wo umgesetzt” mit genau zwei Ausprägungen: Gerät oder Umgebung/Betreiber

Damit erzielst du den Effekt “Stand der Technik = kompensierende Maßnahmen”, ohne dich in CR-Details zu verlieren.

Wenn du den “Kontrast” noch schärfer machen willst, kannst du in einem Nebensatz erwähnen, dass es nicht-IP-Protokolle gibt, die Security integriert haben (z. B. WirelessHART mit Schlüsselmanagement und Verschlüsselung), während der klassische 4–20 mA/HART Pfad das nicht bietet ([fieldcommgroup.org][4])

[1]: https://www.vega.com/api/sitecore/DocumentDownload/Handler?documentContainerId=1008754&documentGroupId=1007792&fileExtension=pdf&languageId=2&softwareVersion=&version=06-03-2023&utm_source=chatgpt.com "IT security guidelines - VEGAPULS 6X"
[2]: https://support.industry.siemens.com/cs/attachments/109988966/s71500_iec_62443_4_2_conformity_de-DE_de-DE.pdf?utm_source=chatgpt.com "IEC 62443-4-2 Konformitätsdokument für S7-1500/ ..."
[3]: https://fcc.report/FCC-ID/O6QPS6XW/5634722.pdf?utm_source=chatgpt.com "Operating Instructions - VEGAPULS 6X"
[4]: https://www.fieldcommgroup.org/sites/default/files/imce_files/technology/documents/WirelessHART%20security%20v1.0.pdf?utm_source=chatgpt.com "Intrinsically Secure WirelessHART® Field Device Networks ..."




------------------------------------------------------------------------------
Was du geschrieben hast gefällt mir sehr gut. Danke.

Jetzt würde ich noch gerne einen Absatz schreiben, warum es jetzt möglich ist Krypto berechnungen zu machen. 
Dieser Absatz folgt auf den letzten absatz (Verbleibende Lücken auf Protokollebenen) und greift nochmal das thema von davor auf, wo erklärt wird warum krypto berechnungen performancetechnisch problematisch sind.
Dieser Absatz soll so ein kleiner Lichtblick sein, bzw. verdeutlichen warum man jetzt krypto machen kann.

Dort kannst du auch gerne auf das Thema Secure Element eingehen, das habe ich vergessen. 
Der Text muss keinesfalls gleich bleiben, du hast freie Hand beim formulieren. 
Lediglich einen Performance vergleich zwischen HW und SW hätte ich gerne drin.

Ein etablierter Ansatz \todo{Formulierung}, um den Zielkonflikt zwischen Performance und Energieverbrauch zu entschärfen, ist der Einsatz dedizierter Krypto-Peripherie bzw.~ Hardwarebeschleuniger. 
Hierbei werden rechenintensive Primitive wie AES, SHA oder ECC in eigenständigen Hardwareblöcken implementiert, die speziell auf diese Operationen hin optimiert sind und deutlich weniger Taktzyklen sowie weniger Energie pro Operation benötigen als eine reine Software-Implementierung. %\cite{banerjee_energy-efficient_2017,panic_embedded_2016,rozlomii_hardware_2024}
Beispielhafte Messungen für einen STM32U3-Mikrocontroller zeigen diesen Effekt deutlich:
Für AES-128 im Galois/Counter Mode (GCM) wird in der dedizierten Krypto-Hardware ein Datendurchsatz von etwa
9{,}17~\si{\mega\byte\per\second} erreicht, während eine reine Software-Implementierung auf demselben Controller lediglich etwa 0{,}76~\si{\mega\byte\per\second} erzielt.
Für SHA-256 liegen die gemessenen Durchsätze bei 45{,}87~\si{\mega\byte\per\second} in Hardware gegenüber 1{,}355~\si{\mega\byte\per\second} in Software \cite{oryx_embedded_benchmark_nodate}.
Somit ist die Verarbeitung in Hardware ca. 12- bzw.~ 34-mal schneller als in Software.
Während diese Werte natürlich von Controller, Krypo-Peripherie und Implementierung des Algorithmus abhängen, zeigen sie doch deutlich, um welche Größenordnung die Aktionen beschleunigt werden können.
Somit werden auch auf eigentlich leistungsschwacher, energieoptimierter Hardware kryptographische Operationen in vertretbarer Zeit ausführbar, sobald geeignete Hardwarebeschleuniger vorhanden sind. \todo{Wie verhält sich der Energieverbrauch dabei?}


Ein zusätzlicher Vorteil integrierter Krypto-Peripherie liegt in der verbesserten Sicherheit des Gesamtsystems. 
Moderne Mikrocontroller für Industrie- und IoT-Anwendungen kombinieren Hardwarebeschleuniger für symmetrische und asymmetrische Kryptographie mit weiteren Sicherheitsfunktionen wie sicherer Schlüsselerzeugung, zertifizierten Entropiequellen, geschützten Schlüsselspeichern, Anti-Tampering-Mechanismen und sicheren Boot-Mechanismen.
Damit bilden sie die Grundlage dafür, auch in nicht IP-basierten Feldgeräten zertifikatsbasierte Identitäten und kryptographisch gesicherte Verbindungen zu realisieren, ohne die strengen Vorgaben an den Energieverbrauch und die Echtzeitfähigkeit zu verletzen.

---------------

\paragraph{Kryptografie als praktikable Option auf modernen Feldgeräten}
Die vorherigen Abschnitte zeigen, dass nicht IP-basierte Feldgeräte heute häufig keine protokollseitige Absicherung von Integrität, Vertraulichkeit und Authentizität bieten und dass diese Lücke in der Praxis überwiegend durch physische und organisatorische Maßnahmen kompensiert wird.
Gleichzeitig haben sich die technischen Rahmenbedingungen in den letzten Jahren deutlich verschoben: Moderne Industrie- und IoT-Mikrocontroller integrieren dedizierte Krypto-Peripherie, sodass kryptografische Verfahren nicht mehr zwangsläufig im Widerspruch zu den typischen Restriktionen (begrenzte Rechenleistung, enger Energiehaushalt, Echtzeitanforderungen) stehen.

Ein etablierter Ansatz zur Entschärfung dieses Zielkonflikts ist die Auslagerung rechenintensiver Primitive in Hardwarebeschleuniger.
Hierbei werden Operationen wie AES (inkl.\ Betriebsmodi wie GCM/CCM) und SHA-256 in spezialisierten Hardwareblöcken ausgeführt, wodurch sowohl die benötigten CPU-Taktzyklen als auch die aktive Laufzeit des Prozessorkerns deutlich sinken.
Beispielhafte Messungen auf einem STM32U3 verdeutlichen die Größenordnung: Für AES-128-GCM erreicht die Hardware etwa 9{,}17~\si{\mega\byte\per\second}, während eine Software-Implementierung auf demselben Controller bei etwa 0{,}76~\si{\mega\byte\per\second} liegt; für SHA-256 wurden 45{,}87~\si{\mega\byte\per\second} (Hardware) gegenüber 1{,}355~\si{\mega\byte\per\second} (Software) gemessen \cite{oryx_embedded_benchmark_nodate}.
Das entspricht einer Beschleunigung um etwa den Faktor 12 bzw.~34.
Für den Energiehaushalt ist dabei nicht nur die Effizienz der Hardwareoperation selbst relevant, sondern vor allem die verkürzte Aktivzeit: Wenn kryptografische Berechnungen schneller abgeschlossen sind, kann der Mikrocontroller früher in stromsparende Zustände zurückkehren, und zeitkritische Funktionen werden weniger lange durch CPU-Last blockiert.

Ergänzend dazu werden Secure Elements oder vergleichbare geschützte Ausführungsumgebungen eingesetzt, wenn langfristige Schlüssel und Identitäten auch gegen Softwarefehler und physische Angriffe abgesichert werden müssen.
Sie trennen Schlüsselmaterial und sicherheitskritische Operationen (z.\,B. Signaturen oder Schlüsselaustausch) vom Anwendungsprozessor, sodass private Schlüssel idealerweise weder im Klartext im Hauptspeicher erscheinen noch durch die Applikation direkt verarbeitet werden.
Je nach Plattform ist dies als separater Baustein oder als integrierte Sicherheitsfunktion des Mikrocontrollers realisiert.

Damit entsteht ein neuer Handlungsspielraum: Obwohl klassische nicht IP-basierte Feldbusprotokolle weiterhin kaum Security-Funktionen bereitstellen, ist es heute technisch und energetisch realistisch, kryptografisch abgesicherte Geräteidentitäten und gesicherte Sitzungen auch in energieoptimierten Feldgeräten umzusetzen.
Diese Entwicklung bildet die Grundlage für die nachfolgenden Kapitel, in denen ein entsprechender Ansatz konzipiert und auf die Randbedingungen nicht netzwerkfähiger Feldgeräte angepasst wird.
