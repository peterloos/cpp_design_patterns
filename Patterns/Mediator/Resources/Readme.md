# Mediator Pattern

## Wesentliche Merkmale

#### Kategorie: *Behavioral Pattern*

#### Ziel / Absicht:

Das *Mediator Pattern* ist ein Verhaltensentwurfsmuster, das die lose Kopplung von Objekten propagiert,
indem Klassen nicht mehr direkt miteinander kommunizieren m�ssen.
Stattdessen werden Mediatorobjekte verwendet, um die Interaktionen zwischen Klassen zu kapseln
und zu zentralisieren.

#### Problem:

Nicht selten bestehen Programme - zumindest in Teilen - aus umfangreichen Klassen.
Dies ist nicht ungew�hnlich, aber es kommt zu Problemen, wenn diese Klassen miteinander kommunizieren m�ssen.
Bei Verwendung des traditionellen Ansatzes, wenn Klassen direkt kommunizieren,
m�ssen diese Klassen ihre internen Implementierungen kennen bzw. im Zuge der Kommunikation offenlegen.

Dies f�hrt zu der bekannten Beobachtung, da es zunehmend schwieriger, die Implementierung einer Klasse zu lesen und zu verstehen,
wenn das Programm immer komplexer wird. Derartige Klassen sind eng miteinander verbunden,
was aus konzeptioneller Sicht nicht gut ist.

#### L�sung:

Das *Mediator Pattern* l�st dieses Problem. In diesem Muster ist die Kommunikation zwischen Objekten in einem Mediatorobjekt gekapselt.
Anstatt dass Klassen direkt kommunizieren, senden Klassen Nachrichten an den Mediator und der Mediator sendet
diese Nachrichten an die anderen Klassen.

#### Struktur (UML):

Das folgende UML-Diagramm beschreibt eine Implementierung des *Mediator Patterns*.
Es besteht im Wesentlichen aus vier Teilen:

  * **ColleagueBase**: Abstrakte Klasse (oder Schnittstelle) f�r alle konkreten Komponenten, auch im Jargon dieses Musters als "*Kollegen*" bezeichnet.
   *Kollegen* sind Klassen, die Gesch�ftslogik enthalten. Jede Komponente hat einen gesch�tzten (`protected`) Verweis auf einen Mediator,
   der mit dem Typ der Mediatorschnittstelle deklariert ist (`MediatorBase`).
   Der *Kollege* kennt folglich die tats�chliche Klasse des Mediators nicht.
   Sie k�nnen die Komponente (Kollege) daher in anderen Programmen wiederverwenden,
   indem Sie sie mit einem anderen Mediator verkn�pfen.
  * **ConcreteColleague**: Eine Implementierung der `ColleagueBase`-Klasse. Konkrete Kollegen sind Klassen,
   die miteinander kommunizieren. *Kollegen*
   sollten keine anderen Komponenten kennen. Wenn innerhalb oder mit einer Komponente etwas Wichtiges passiert,
   muss diese nur den Mediator benachrichtigen.
   Wenn der Mediator die Benachrichtigung erh�lt, kann er den Absender leicht identifizieren, 
   was ausreichend sein sollte,
   um zu entscheiden, welche Komponente(n) im Gegenzug zu aktivieren ist (sind) - Aufruf einer Methode.
  * **MediatorBase**: Abstrakte Klasse (Schnittstelle) f�r das `Mediator`-Objekt.
   Diese Klasse enth�lt Methoden, die von Kollegen verwendet werden k�nnen.
   Die Mediator-Schnittstelle deklariert Kommunikationsmethoden f�r Komponenten,
   in der Regel sind dies nur wenige Benachrichtigungsmethoden.
   Komponenten k�nnen jeden Kontext als Argument dieser Methode �bergeben,
   einschlie�lich eines Verweises auf sich selbst (`this`),
   jedoch ist dabei zu beachten, dass keine Kopplung zwischen einer empfangenden Komponente und der Klasse des Absenders entsteht.
  * **ConcreateMediator**: Implementierung der Methoden der `MediatorBase`-Klasse.
   Diese Klasse enth�lt Verweise auf alle Kollegen, die miteinander kommunizieren m�ssen.
   Konkrete Mediatoren kapseln die Beziehungen zwischen verschiedenen Kollegen.

<img src="dp_mediator_pattern.svg" width="800">

Abbildung 1: Schematische Darstellung des *Mediator Patterns*.


#### Conceptual Example:

*Hinweis*:

Das *Conceptual Example* liegt in drei Varianten vor:

  * Variante 1: klassisch - d.h. mit "raw"-Zeigern.
  * Variante 2: Wie Variante 1, aber mit `std::shared_ptr` Objekten und `std::enable_shared_from_this<>` Mechanismus.
  * Variante 3: Prinzipiell wie Variante 2, nur: Die Entscheidung, welche empfangende Komponente
    aufzurufen ist, wird dieses Mal �ber das Absenderobjekt getroffen (und nicht �ber eine Parameterkennung).

[Quellcode 1](../ConceptualExample01.cpp)

[Quellcode 2](../ConceptualExample02.cpp)

[Quellcode 3](../ConceptualExample03.cpp)

---

Die Anregungen zum konzeptionellen Beispiel finden Sie unter

[https://refactoring.guru/design-patterns](https://refactoring.guru/design-patterns/mediator/cpp/example#lang-features)

und

[https://www.codeproject.com](https://www.codeproject.com/Articles/455228/Design-Patterns-3-of-3-Behavioral-Design-Patterns#Mediator)

vor.

---

[Zur�ck](../../../Resources/Readme_05_Catalog.md)

---
