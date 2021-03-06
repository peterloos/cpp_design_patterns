# Iterator Pattern

## Wesentliche Merkmale

#### Kategorie: *Behavioral Pattern*

#### Ziel / Absicht:

Das *Iterator Pattern* ist ein Entwurfsmuster,
das es erm�glicht, die Elemente eines Aggregatobjekts ohne Kenntnis seiner Struktur sequentiell
zu durchlaufen (zu *traversieren*).
Auf diese Weise wird das Traversieren von Listen, B�umen und anderen Containerstrukturen
in einer standardisierten Weise erm�glicht.

#### Problem:

Eine *Collection* ist eine der am h�ufigsten verwendeten Datenstrukturen in der Programmierung.
Eine *Collection* stellt einen *Container* f�r eine Gruppe von Objekten dar:

<img src="dp_collections_iterator.png" width="600">

Abbildung 1: Unterschiedliche Arten von *Collections*.

Die meisten Collections speichern ihre Elemente in einfachen linearen (verketteten) Listen ab.
Wiederum andere basieren auf komplexeren Datenstrukturen wie Stapeln (Stack), B�umen (Tree), Diagrammen oder anderen.
Unabh�ngig davon, wie eine Collection strukturiert ist,
sollte sie eine M�glichkeit bieten, ihre Elemente durchlaufen (traversieren) zu k�nnen,
so dass ein anderer Code diese Elemente verwenden kann.
Es versteht sich dabei von selbst, dass bei einem derartigen Durchlauf kein Element 
mehrfach oder �berhaupt nicht erfasst werden darf.

Dies mag nach einer einfachen Aufgabe klingen, wenn die Elemente beispielsweise in einem Array
oder einer listenartigen Struktur abgelegt sind.
Es werden einfach alle Elemente der Reihe nach (Index eines Arrays, *next*-Zeiger in einer Liste) erfasst.
In einer komplexen Datenstruktur wie beispielsweise einer Baumstruktur
ist dies nicht so einfach! Hier gibt es zum Beispiel 
den "*Depth-First Traversal*" oder "*Breadth-First Traversal*" Algorithmus,
die bzgl. der Reihenfolge des Durchlaufens der Baumstruktur sehr unterschiedlich funktionieren:

<img src="dp_collections_iterator_tree_structures.png" width="600">

Abbildung 2: Eine Collection kann auf verschiedene Arten durchlaufen werden.

#### L�sung:

Die Kernidee des *Iterator Patterns* besteht darin,
die Art und Weise des Durchlaufs einer Collection in ein separates Objekt zu extrahieren, das als *Iterator* bezeichnet wird.

Alle Iteratoren m�ssen dieselbe Schnittstelle implementieren.
Dadurch ist ein Clientcode mit jedem Typ von Collection oder jedem Traversierungsalgorithmus kompatibel,
sofern ein *Iterator*-Objekt vorhanden ist.

M�chte man eine Collection auf eine bestimmte Art und Weise durchlaufen
(z.B. "*Depth-First Traversal*" oder "*Breadth-First Traversal*"),
implementiert man einfach eine neue Iteratorklasse.
So muss man weder �nderungen an der Collection oder am Client vornehmen.


#### Struktur (UML):

Das folgende UML-Diagramm beschreibt eine Implementierung des *Iterator Patterns*.
Es besteht im Wesentlichen aus f�nf Teilen:

  * **Client**: Fordert das *Iterator*-Objekt von einem aggregierten Objekt an und "konsumiert" es, wenn die Elemente durchlaufen werden sollen.
  * **AggregateBase**: Abstrakte Basisklasse (oder Schnittstelle) f�r alle konkreten Aggregate. Diese Klasse enth�lt eine Methode, die auf Anfrage ein Iterator-Objekt zur�ckgibt.
  * **ConcreteAggregate**: Repr�sentiert die konkrete Implementierung der `AggregateBase`-Schnittstelle. Hat Zugriff auf die Elemente, die mit dem Iterator durchlaufen werden sollen.
  * **IteratorBase**: Abstrakte Klasse (oder Schnittstelle) eines konkreten Iterators. Enth�lt Methoden (pr�ziser: die Signaturen von Methoden), mit denen die Elemente durchlaufen werden k�nnen.
  * **ConcreteIterator**: Konkrete Realisierung von `IteratorBase`.

<img src="dp_iterator_pattern.svg" width="800">

Abbildung 1: Schematische Darstellung des *Iterator Patterns*.


#### Conceptual Example:

[Quellcode 1](../ConceptualExample01.cpp) - Standard Variante

[Quellcode 2](../ConceptualExample02.cpp) - C++ spezifische Variante

---

Die Anregungen zum konzeptionellen Beispiel finden Sie unter

[https://refactoring.guru/design-patterns](https://refactoring.guru/design-patterns/iterator/cpp/example#example-0)

und 

[https://www.codeproject.com](https://www.codeproject.com/Articles/455228/Design-Patterns-3-of-3-Behavioral-Design-Patterns#Iterator)

vor.

---

[Zur�ck](../../../Resources/Readme_05_Catalog.md)

---
