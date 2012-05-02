JAX Conference Take-Aways
=========================

Time to Market
--------------

<div style="width:425px" id="__ss_12613544"> <strong style="display:block;margin:12px 0 4px"><a href="http://www.slideshare.net/Stephan.Schmidt/what-everyone-should-know-about-time-to-market" title="What everyone should know about time to market" target="_blank">What everyone should know about time to market</a></strong> <iframe src="http://www.slideshare.net/slideshow/embed_code/12613544" width="425" height="355" frameborder="0" marginwidth="0" marginheight="0" scrolling="no"></iframe> <div style="padding:5px 0 12px"> View more <a href="http://www.slideshare.net/" target="_blank">presentations</a> from <a href="http://www.slideshare.net/Stephan.Schmidt" target="_blank">Stephan Schmidt</a> </div> </div>

Time to market = Zeit zwischen der Idee und den ersten Einnahmen

Time to market is a huge lever
(Technology isn't)

"In der Software-Industrie gibt es zu wenige Fakten und zu viele Meinungen"

Buffers are the biggest driver

Time to Market = Front-Up + Entwicklung

Alle fokussieren auf die Entwicklung
Die Probleme liegen aber im Front-Up

Buch: Reinertsen (1998) "Developing Products in half the time"

Market opportinity and Gefühl der Dringlichkeit verlaufen gegensätzlich

Development is a solved problem in an agile process

Advice: Measure!!!

Low quality and rework is one of the highest wastes in software development

Serial production trumps parallel production

In-Sourcing of Software Development
-----------------------------------

Within 6 months
2 internal, 2 external developers
process: Scrum

Fixed price contracts kill software quality

developer time is precious.
--> Using SaaS and IaaS offers as much as possible

 * GitHub
   "GitHub is the Facebook for nerds."

 * Jenkins + Artifactory as IaaS

 * Monitoring via New Relic
 * Continuous Search Monitoring via SirApp
 * Log Monitoring: Party Gorilla / GrayLog2
 * Feature tracker: After Agilofant, they use Redmine

Teams prefer a physical task board

SaaS tools help making teams agile faster


Verlernte Agilität: schleichende Fehler in agilen Prozessen
-----------------------------------------------------------

Sebastian Bauer (@litervollmilch)

1. problem: product backlog
 * too many stories
 * no non-functional requirements

 => clean up the backlog
 => communicative stories
 => Don't over-specify, let the team breathe
 => Involve the team
 => Alles abbilden, estimate every item

2. problem: Product Owner
 * empowerment is undermined

 => PO must be available
 => dedicated, full-time
 => the ScrumMaster should stärken den PO over and over again, up (higher mgmt) and down (team) the hierarchy
 => Verindere micro-management, protect self-organization

3. problem: ScrumMaster
 * takes over team tasks, loses his focus on impediments
 * takes over PO tasks
 * disciplinary boss

 => Fels in der Brandung; Selbstreflexion und Feedback
 => dediziert, Vollzeit
 => Rollenkonflikte vermeiden
 => "Spürhung" für Impediments

4. problem: Daily Scrum
 * wird häufig langweilig, nutzlos
 * Report an den PO
 * Vorlesen der Todos von gestern
 * verkommt zur Rechtfertigung

 => tägliches Strategie-Meeting
 => Aufstehen! Vors Scrum-Board!
 => Tempo!
 => Timebox!
 => Fokus auf wertvolle Inhalte

5. problem: Impediments
 * werden hingenommen
 * werden nicht (mehr) aus dem Weg geräumt

 => Warnehmung schärfen
 => Nichts akzeptieren
 => Nichts rechtfertigen
 => Alles, wirklich ALLES beseitigen

6. problem Sprint Planning
 * PO beeinflusst die Schätzungen
 * Velocity wird überschätzt
 * Zu großes Commitment
 * Schätzungen (Planning Poker) steigen an
 * dauert zu lange

 => Team mit Über-Optimismus konfrontieren
 => PO im Zaum halten
 => Kein Übergabe-Meeting für neue, unbekannte Anforderungen

7. Sprint Review
 * Definition of Done wird nicht berücksichtigt
 * PO nimmt "done" Stories nicht ab

 => Definition of Done konsequent anwenden / überprüfen
 => Offene Punkte protokollieren
 => Unfertiges gehört hier *nicht* hin
 => PO-Wunschkonzert vermeiden

8. problem: Retrospektiven
 - werden abgeschafft
 - Kein empirisches Vorgehen (Messen, Überprüfen)
 - Dieselben Aktivitäten werden wiederholt (z.B. Mad, Sad, Glad)

 => Feedback sammeln
 => Emotionales Eis brechen (z.B. durch Abwechslung)
 => Konflikte offen austragen; Team aus "Stillphasen" heraustreiben
 => Empirisch vorgehen; Fortschritte kontrollieren und steuern

9. problem: Timeboxes
 => Konsequent einhalten
 => Timeboxes "aus Gründen"
 => zwingen zur Selbst-Organisation

Einflussfaktoren von außen
 - Definierte Deadlines mit definiertem Umfang
 - "Ihr müsst doch schneller werden"
 - Misstrauen
 - Doppelbelsatung, z.B. in zwei Projekten / Multitasking

SCRUM IST
 - ein sensibles Ökosystem
 - REVOLUTION!
 - kein sklavischer gehorsam
 - empirisch

Lean Startup
------------

by @StefanRoock

Buch: Steve Blank, Bob Dorf: "The Startup owners manual"

Risiken
 - Realisierung
 - Kundenbedürfnisse

Lean Startup: Realisierung ist kein Problem mehr, sondern die Kundenbedürfnisse
zu realisieren / befriedigen

Mehr als 60 % der Features werden nie benutzt, sowohl bei Standard-Software (MS Word), wie auch bei In-House-Systemen

       Systemfunktion  !=  Kundenbedürfnis
z.B.   Digitaluhr     vs.  Analoguhr

=> Annahmen müssen überprüft werden

Pivot: z.B. flickr: vom Online-Spiel zum Foto-Dienst

Am Anfang: viel Pivot notwendig; psychologisch anspruchsvoll

Lernen pro Zeiteinheit muss maximiert werden

"Würdet ihr euer eigenes Geld in die (Weiter-)Entwicklung des Produktes stecken?" (Kent Beck)

Das EXPERIMENT
 - Maximale Isolation von it-agile (eigenes Büro, Autoreply für die E-Mail, etc.)
 => Wenn Startup, dann richtig (eigene GmbH, Büros, ...)
    vgl. auch Apple bei der Entwicklung neuer Produkte

MVP: Minimales brauchbares Produkt, aber 'brauchbar' für wen?

RIES: MVP = smalles product to execute build-measure-learn cycle

"Wenn es dir nicht peinlich ist, hast du es zu spät released."

Mehr als 15 Releases pro Tag => Continuous Deliver

Live Metriken
Erkenntnis: Werbung bei Facebook ist effektiver als bei Google

wenige Benutzer -> Nutzlose Metriken

Man muss seinen eigenen Einfluss rausrechnen!

Wenn keine objektiven Messungen möglich sind, muss man das persönliche Gespräch suchen.
=> Sehr reichhaltiges Feedback

Roock's Marmeladen-Regel: "Je metrischer man wird, desto dünner wird das Feedback"

### Erkenntnisse
Wenn Time to Market/Lead-Time verlässlich unter zwei Tagen liegt, braucht man keinen Prozess.
Ein ProductOwner wäre schädlich gewesen.

## Abschluss-Panel
 - Bei Impediments -- egal ob Scrum oder Kanban -- "Wenn es schwierig wird, muss man da durch."
 - Bei Festpreisprojekten _auf jeden Fall_ Scrum machen
 - Bei Festpreisprojekten leidet die Software-Qualität
 - Kunden vermitteln, dass Festpreisprojekte große Nachteile für ihn haben.
 - Festpreis als Indikator für ein Vertrauensproblem.
 - Spezialisierung vs. Generalisierung der Team-Mitglieder ist eine Entscheidung des Teams => Selbstorganisation!
 - SLack-Time kann man zur Generalisierung nutzen.
