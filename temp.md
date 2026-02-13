Ich möchte jetzt ein Kapitel über den Stand der Technk bei ethernetbasierten Feldgeräten schreiben.

Es soll nicht so umfangreich sein, wie das über nicht ethernetbasierte Feldgeräte, aber einen guten Überblick darüber gehen. 
Vor alles soll es auch die für meine Thesis relevanten Themen beinhalten.
Der Konzept sicherer Verbindungsaufbau wie in meiner Thesis erarbeitet wird, existiert ja dort teilweise schon (glaube ich).
Ich habe eine Sammlung an Themen die rein könnten, falls es passt. Wenn du Nachfragen hast, frag mich gerne.

Themen die enthalten sein können, je nach dem ob es passt:
## Stoffsammlung
### PROFINET - Zukünftige OT-Security
 Klasse 1 – umgangssprachlich „Robustness“ bietet drei Kernfunktionalitä ten, die eine schrittweise Verbesse rung des bestehenden Zonenschutzes ermöglichen. #k232 
- Security-Klasse 2 gewährleistet, dass Angreifer keine unbemerkten Manipulationen an PROFINET-IO-Daten vornehmen können. Die Klasse 3 bietet zusätzlich Verschlüsselung, sodass eine Interpretation der Daten durch Angreifer nicht möglich ist. Der Kern der Security-Klasse 2 ist die Absicherung der PROFINET-Application Relation (AR) zwischen Controller und Device, wobei sich beide Endpunkte beim Hochlauf gegenseitig über X.509- Zertifikate [13] authentifizieren. Hier wird das Protokoll EAP-TLS sowohl für Security-Klasse 2 als auch für Security- Klasse 3 verwendet. Nach erfolgreicher Authentisierung handeln beide Teilnehmer einen gemeinsamen symmetrischen Schlüssel für die Datenübertragung der Record-Daten, I/O-Daten und Alarme aus. Zur Aufrechterhaltung eines hohen Schutzniveaus wird der symmetrische Schlüssel während der Kommunikation in regelmäßigen Abständen aktualisiert. #k232 
- Ethernet-APL ist ein Zweidraht-Ethernet, welches Feldgeräte sowohl mit Daten als auch mit Energie versorgt.  #k232 
- Für Automatisierungssysteme mit typischen Anforderungen geht der VDMA bei einem Leitfaden [23] von einem Security-Level 2 aus. #k232 
- Ein Ethernet-APL-Messumformer ist in die Kategorie „Eingebettetes Gerät (EDR)
- Durch den Einsatz eines PROFINET-Protokollstacks mit Security-Funktion kann diese Forderung (Systemintegrität) für die PROFINET-Schnittstelle erfüllt werden. Das gleiche gilt für die OPC-UA-Schnittstelle und für die WebServer-Schnittstelle. Hier stehen jeweils sichere Protokollvarianten zur Verfügung. #k232 
- Die Vertraulichkeit von Daten ist in der OT-Security, im  Gegensatz zur IT-Security, von geringerer Bedeutung, weil Prozessdaten in der Regel einen geringen Schutzbedarf in Bezug auf die Vertraulichkeit haben. Dennoch wird dieses Thema in der Norm adressiert. Zum einen in Bezug auf den Schutz von ruhenden Daten, für die eine Leseberechtigung erforderlich ist, zum anderen in Bezug auf das Löschen von Daten, für die eine Leseberechtigung vorgesehen ist. #k232 
1. Anforderung ist für einen Ethernet-APL Messumformer irrelevant: Z. B. Notstromversorgung, Schutz der Zonengrenze #k231 #k232
2. Anforderung ist relevant und durch das PROFINET-Security Konzept abgedeckt: Z. B. Integritätsschutz der Kommunikation, Vertraulichkeitsschutz der Kommunikation. #k231 #k232
3. Anforderung ist relevant, aber vom Feldgerät abhängig: Z. B. Integritätsschutz der Software beim SW-Update, Integrität des Boot-Prozesses (engl. Secure-Boot), etc. #k231 #k232


%%%%%%%%%%%%%%%%%%%%%%%%%%%%% Gesetzt %%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
% Stand der Technik bei nicht netzwerkfähigen Feldgeräten
\subsection{Stand der Technik bei nicht netzwerkfähigen Feldgeräten}
\label{2_4_1_Stand_Technik_Non_IP}
Für nicht netzwerkfähige Feldgeräte sehen die zugehörigen Feldbusstandards keinerlei Security-Maßnahmen vor.
Keiner der gängigen Feldbusse, weder HART, PROFIBUS PA, OPC noch MODBUS unterstützt Sicherheitsfunktionen in Bezug auf Integrität, Verschlüsselung oder Authentifizierung. Auch ist nicht davon auszugehen, dass sich dies in absehbarer Zeit ändern wird \cite{bsi_-_bundesamt_fur_sicherheit_in_der_informationstechnik_ics-security-kompendium_2014}\cite{niemann_ot-sicherheitsanforderungen_2022}.

Die Ursachen für das Fehlen protokollseitiger Sicherheitsmechanismen sind vielfältig und historisch gewachsen.

% PASS
% Physischer Schutz und Air Gaps
\paragraph{Physischer Schutz und Air-Gaps}
ICS-Anlagen befinden sich in der Regel in physisch abgesicherten Bereichen, die durch Zäune, Mauern oder vergleichbare Barrieren geschützt sind.
Der Zugang zu den Feldgeräten ist dabei auf das vor Ort tätige Betriebspersonal sowie auf externe Dienstleister, etwa für Inbetriebnahme oder Wartung, beschränkt \cite{niemann_ot-sicherheitsanforderungen_2022}.
Zusätzlich wurden insbesondere ältere Anlagen häufig physisch von anderen Netzwerken isoliert, um sie vor Cyberangriffen zu schützen.
Da sich die Geräte in einem abgeschotteten Bereich befanden und nicht von außen erreichbar waren, wurde lange Zeit argumentiert, dass dieser Schutz ausreichend sei \cite{bsi_-_bundesamt_fur_sicherheit_in_der_informationstechnik_ics_2024}.

Diese sogenannten \emph{Air-Gaps}, also die vollständige Trennung von IT und OT, erreichen in der Praxis jedoch selten das angestrebte Schutzniveau.
Häufig ist trotz der physischen Trennung ein Datenaustausch zwischen den Netzen notwendig oder gewünscht, und genau diese Schnittstellen können von Angreifern ausgenutzt werden, um die Isolation zu überwinden \cite{bsi_-_bundesamt_fur_sicherheit_in_der_informationstechnik_ics_2024}.
Darüber hinaus ist eine vollständige Trennung der OT von der IT heute nur noch in Ausnahmefällen und bei besonders hohem Schutzbedarf umsetzbar.
Mehrstufige Produktionsprozesse, deren systemübergreifende Steuerung sowie regulatorische Vorgaben erfordern zunehmend eine Vernetzung der OT, auch über Organisationsgrenzen hinweg. Verstärkt wird diese Entwicklung durch den Trend zur Optimierung von Fertigungsprozessen im Kontext von Industrie 4.0 \cite{deutschland_it-grundschutz-kompendium_2023}.

Selbst bei ausreichender Absicherung der OT und einem physischen Zugangsschutz bestehen weiterhin Risiken den Angreifer von innen mit direktem Zugriff auf das Automatisierungsnetzwerk oder das Feldgerät könnten gezielt Schwachstellen ausnutzen.
Eine Studie von Bitkom zeigt, dass interne Bedrohungen eine erhebliche Gefahr darstellen: 62\,\% der Angriffe auf deutsche Unternehmen gehen von aktuellen oder ehemaligen Mitarbeitern aus \cite{streim_spionage_2017}.
Mit entsprechendem Zugang wäre es beispielsweise möglich, ein Feldgerät unbemerkt durch ein manipuliertes Gerät auszutauschen.

Darüber hinaus gibt es Einsatzszenarien, in denen ein flächendeckender physischer Schutz nicht realisierbar ist.
Auch wenn das Feldgerät selbst und zugehörige Komponenten wie Gateways vor unbefugtem Zugriff geschützt sind, können Verbindungsleitungen, insbesondere bei größeren Distanzen, ungeschützt verlaufen.
Ein charakteristisches Beispiel ist die Füllstandsmessung an einem Stausee oder Überlaufbecken, wo die Messleitungen über längere Strecken außerhalb kontrollierten Bereichs verlaufen können.


%Technische Einschränkungen
\paragraph{Technische Einschränkungen}
Neben den physischen Schutzmaßnahmen spielen auch technische Limitierungen eine wesentliche Rolle für das Fehlen protokollseitiger Sicherheitsmechanismen.

Viele der heute eingesetzten Feldgeräte stammen aus einer Zeit, in der Cybersicherheitsbedrohungen noch nicht in dem heutigen Ausmaß existierten.
Diese Legacy-Systeme verfügen weder über die erforderliche Hardware noch über die Softwareunterstützung, um moderne Sicherheitsverfahren umzusetzen.
Da Anlagen im OT-Umfeld häufig über mehrere Jahrzehnte betrieben werden, ist eine große installierte Basis solcher Geräte nach wie vor im Einsatz \cite{stouffer_guide_2023}.

Kryptografische Verfahren, insbesondere asymmetrische Algorithmen, sind ohne dedizierte Krypto-Peripherie vergleichsweise rechenintensiv.
Zusätzlicher Rechenaufwand aufgrund Berechnung kryptographischer Operationen würde die verfügbare Verarbeitungszeit zusätzlich beanspruchen und steht damit in direktem Konflikt mit den begrenzten Ressourcen der Feldgeräte \cite{mclaughlin_cybersecurity_2016}.

Kryptographische Operationen, stehen zudem auch im Konflikt mit dem Energieverbrauch der Fedlgeräte.
Nicht netzwerkfähige Feldgeräte sind häufig für besonders robuste und energieeffiziente Betriebsbedingungen ausgelegt.
Bei 2-Draht-Geräten muss die gesamte Elektronik aus dem begrenzten Energiehaushalt der \SI{4}{\milli\ampere}--\SI{20}{\milli\ampere}-Stromschleife versorgt werden.
Abzüglich Toleranzen und Reserven stehen dabei lediglich ca.\ \SI{3,5}{\milli\ampere} für die interne Elektronik zur Verfügung \cite{johnson_power_2013}.
Mikrocontroller werden daher häufig mit niedrigen Taktraten betrieben und die verfügbaren Ressourcen auf das für Messwerterfassung, Signalverarbeitung, Diagnose und Kommunikation notwendige Minimum optimiert.
Zwischen Verarbeitungsdauer, Energieverbrauch und Sicherheitsniveau muss somit stets ein Kompromiss gefunden werden.
In der Konsequenz wurden Sicherheitsmechanismen in vielen Feldgeräten entweder gar nicht vorgesehen oder auf einfache Schutzfunktionen wie Schreibschutz, PIN-basierte Sperren oder rein organisatorische Maßnahmen beschränkt \cite{bsi_-_bundesamt_fur_sicherheit_in_der_informationstechnik_ics_2024}.

%% Umsetzung der Maßnahmen
\paragraph{Einordnung nach IEC 62443 und kompensierende Maßnahmen}
In der IEC-62443-Familie werden Sicherheitsanforderungen für Komponenten im Kontext eines übergreifenden Zonen- und Leitungsmodells betrachtet.\todo{Security in Depth?}
In der industriellen Praxis wird dabei häufig davon ausgegangen, dass Schutzmaßnahmen für einfache Komponenten nicht ausschließlich durch das Feldgerät selbst, sondern durch kompensierende Maßnahmen in der Umgebung erreicht werden.
Insbesondere Security Level 2 wird in vielen Industriepublikationen als das niedrigste Niveau eingeordnet, ab dem Schutz gegen vorsätzlichen Missbrauch adressiert wird \cite{niemann_profinet_2025}.
Dies verdeutlicht die Lücke zwischen klassischen Feldgeräteprotokollen ohne integrierte Security-Funktionen und den Anforderungen, die bei gezielten Angriffen typischerweise relevant werden.

%Security Guideline 6X
\paragraph{Praxisbeispiel: Security-Umsetzung bei einem nicht netzwerkfähigen Feldgerät}
Am Beispiel eines 2-Draht-Feldgeräts (VEGAPULS 6X mit 4~\dots~20\,mA/HART) zeigt sich, dass Sicherheitsfunktionen in der Praxis stark auf lokale Schutzmechanismen und organisatorische Maßnahmen verteilt werden.
Die zugehörige Security Guideline \cite{vega_grieshaber_kg_it-sicherheitsrichtlinien_nodate} weist explizit darauf hin, dass das standardisierte HART-Protokoll keinen ausreichenden Schutz gegen Datenmanipulation und Spionage bietet und deshalb nur in einer Umgebung mit Schutzniveau entsprechend SL1 bzw. bei sichergestelltem physischem Zugriffsschutz auf die Signalleitungen betrieben werden soll.
Für Schnittstellen und den Gerätezugang werden daher Maßnahmen wie Zugriffsschutz per Passwort, Deaktivierung ungenutzter Kommunikationskanäle sowie physische Sicherungen (z.\,B. Verplombung) gefordert.
Geräteseitig werden zudem Funktionen wie Firmware-Integritätsprüfungen, Ereignisspeicher und Ressourcenmanagement als Sicherheitsfunktionen genannt.
Diese Maßnahmen erhöhen die Härtung des Geräts, ersetzen jedoch keinen kryptografisch geschützten Kommunikationskanal auf dem Feldbus.

%Verbleibende Lücken
\paragraph{Verbleibende Lücken auf Protokollebene}
Aus Sicht der Schutzziele Vertraulichkeit und Integrität verbleibt bei nicht netzwerkfähigen Feldgeräten insbesondere eine Lücke in der Ende-zu-Ende-Absicherung der Kommunikation.
Während Integrität im Feldbuskontext häufig nur über einfache Prüfsummen oder CRC-Mechanismen adressiert wird, existieren typischerweise keine Verfahren zur kryptografischen Authentifizierung von Geräten, keine aushandelbaren Sitzungsschlüssel und keine Verschlüsselung der Nutzdaten auf der Leitung.
Damit kann ein Angreifer mit physischem Zugriff auf die Signalleitung Daten mitlesen oder manipulieren, ohne durch das Protokoll selbst zuverlässig detektiert oder ausgeschlossen zu werden.
Genau an dieser Stelle setzt die vorliegende Arbeit an, indem eine gerätebasierte Identität über Zertifikate und ein sicherer Verbindungsaufbau auch für nicht IP-basierte Kommunikationskanäle konzipiert und umgesetzt wird.

%Ausblick
\paragraph{Kryptografie als Option auf modernen Feldgeräten}
Die vorherigen Abschnitte zeigen, dass nicht ethernet-basierte Feldgeräte heute häufig keine protokollseitige Absicherung von Integrität und Vertraulichkeit bieten und das diese Lücke in der Praxis überwiegend durch physische und organisatorische Maßnahmen kompensiert wird.
Gleichzeitig haben sich die technischen Rahmenbedingungen für Feldgeräte in den letzten Jahren deutlich verschoben.
Moderne Mikrocontroller integrieren dedizierte Krypto-Peripherie bzw. Hardwarebeschleuniger, sodass kryptografische Verfahren nicht mehr zwangsläufig im Widerspruch zu den typischen Restriktionen (begrenzte Rechenleistung, enger Energiehaushalt, zeitliche Anforderungen) stehen.
Hierbei werden kryptographische Primitive,\todo{Definition Kryptografische Primitive raussuchen}
in speziell dafür entwickelten Hardwareblöcken berechnet, wodurch einerseits der Przoessor entlastet wird und die kryptographischen Berechnungen deutlich schneller und effizienter berechnet werden \cite{stmicroelectronics_ds14830_2025}.

Beispielhafte Messungen auf einem STM32U3 verdeutlichen die Größenordnung: Für AES-128-GCM erreicht die Hardware\footnote{Hardware bezieht sich auf den HW-Beschleuniger und Software auf die Berechnung mittels CyclonePRO-Softwarebibliothek auf dem Mikrocontroller} etwa 9{,}17~\si{\mega\byte\per\second}, während eine Software-Implementierung auf demselben Controller bei etwa 0{,}76~\si{\mega\byte\per\second} liegt.
Für SHA-256 wurden 45{,}87~\si{\mega\byte\per\second} (Hardware) gegenüber 1{,}355~\si{\mega\byte\per\second} (Software) gemessen \cite{oryx_embedded_benchmark_nodate}.
Das entspricht einer Beschleunigung um etwa den Faktor 12 bzw.~34, während der Energieverbrauch nur leicht steigt \todo{Messungen hinzufügen, oder darauf verweisen}.

Parallel zu dieser Entwicklung im Bereich Hardware, stehen aber auch für Berechnung in Software optimierte Verfahren zur Verfügung, etwa \emph{Curve25519} für Schlüsselaustausch und Signaturen, sowie \emph{ChaCha} als schnelle Alternative für symmetrische Verschlüsselung \cite{paar_understanding_2024}.

Ergänzend dazu werden Secure Elements oder vergleichbare geschützte Ausführungsumgebungen eingesetzt, wenn langfristige Schlüssel und Identitäten auch gegen Softwarefehler und physische Angriffe abgesichert werden müssen.
Sie trennen Schlüsselmaterial und sicherheitskritische Operationen (z.\,B. Signaturen oder Schlüsselaustausch) vom Mikrocontroller, sodass private Schlüssel idealerweise weder im Klartext im Hauptspeicher erscheinen noch durch die Applikation direkt verarbeitet werden.
Je nach Plattform ist dies als separater Baustein oder als integrierte Sicherheitsfunktion des Mikrocontrollers realisiert.
Diese Baugruppen bringen noch weitere Funktionen wie sichere Schlüsselerzeugung, zertifzierte Entropiequellen, Anti-Tampering- und sichere Bootmechanismen mit sich. 

Obwohl klassische nicht IP-basierte Feldbusprotokolle weiterhin kaum Security-Funktionen bereitstellen, ist es heute technisch und energetisch realistisch, kryptografisch abgesicherte Geräteidentitäten und gesicherte Sitzungen auch in energieoptimierten Feldgeräten umzusetzen.
Diese Entwicklung bildet die Grundlage für die nachfolgenden Kapitel, in denen ein entsprechender Ansatz konzipiert und auf die Randbedingungen nicht netzwerkfähiger Feldgeräte angepasst wird.