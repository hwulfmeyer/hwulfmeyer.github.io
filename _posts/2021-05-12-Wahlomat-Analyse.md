---
title: "Analyse des Wahl-O-Mat für die Landtagswahl Sachsen-Anhalt 2021"
categories:
  - Blog
tags:
  - Wahlomat
  - Wahl-o-Mat
  - Landtagswahl
  - Visualisierung
  - Analyse
  - Daten
  - Clustering
  - PCA
---

Dieses Jahr ist Wahljahr in der Bundesrepublik und so auch für den Landtag in Sachsen-Anhalt am 6. Juni.
Dafür wurde auch wieder ein [Wahl-O-Mat veröffentlicht](https://www.wahl-o-mat.de/sachsenanhalt2021/app/main_app.html).

### Darstellung der Antworten
Die Antworten der Partein können auf der Website ausgelesen werden und diese können dann hübsch Visualisiert und mittels Clustering oder PCA sogar analyisiert werden. Genau so wurde das schon von D. Kriesel zur letzten
Bundestagswahl 2017 getan. Siehe [Teil 1 hier](https://www.dkriesel.com/blog/2017/0903_auswertung_des_wahl-o-mats_zu_einer_parteienlandkarte) und 
[Teil 2 hier](https://www.dkriesel.com/blog/2017/0904_wahl-o-mat-auswertung_teil_2_thesen-_und_parteienverwandtschaften). Ich habe mich also von ihm inspirieren lassen 
und habe mich vor ein paar Wochen daran gemacht genau so etwas selber aufzuziehen. Das ganze habe ich wie schon er in einer 'Clustermap' dargestellt.

<img src="https://user-images.githubusercontent.com/9419801/118012930-df98fb80-b351-11eb-84a1-5940b64a0f70.png" alt="clustermap" width="600"/>
<sup>(Hinweis: Die Partei Gesundheitsforschung habe ich manuell entfernt, weil diese für alle Thesen "Neutral" als Antwort gegeben haben)</sup>

Die Spalten sind hier die Partein und in den Zeilen befinden sich die Thesen und die Antworten der Parteien darauf.
Intuitiv steht hier Grün für Zustimmung, Rot für Ablehnung einer These und Grau steht für Neutral. Die Thesen werden hier mit der offiziellen Kurzform des Wahl-O-Mats dargestellt.
Die Kompletten Thesen mit einem Positionsvergleich findet ihr [hier](https://www.wahl-o-mat.de/sachsenanhalt2021/PositionsVergleichSachsenAnhalt2021.pdf). Die kurzformen können manchmal etwas verwirrend sein. So ist z.B. These 10 die Frage nach einem Aufnahmestop für Flüchtlinge, wird aber hier mit "Aufnahme von Flüchtlingen" abgekürzt. 

Grob gesagt sind die Partein hier ihrer Änhlichkeit nach geordnet, also wie Ähnlich sind die Antworten einer Partei zu einer anderen. Das ganze basiert auf einem Clustering Verfahren, das sich [hierarchical/agglomerative clustering](https://de.wikipedia.org/wiki/Hierarchische_Clusteranalyse) nennt. Es versucht kurzgefasst die Partien und Thesen zu Gruppieren. Das Verfahren benutzt eine Distanzmetrik wie zum Beispiel den Euklidischen Abstand. Jede These wird dabei als eine Dimension betrachtet und die Antwortmöglichkeiten dann als der Wertebereich (-1,0,1) den diese annehmen können.  
Normalerweise würden für n Parteien dann n<sup>(1-n)</sup> verschiedene Distanzen herauskommen, also jede Partei zu jeder anderen und um das Verwertbar darstellen zu können wird dann das Clustering verwendet. Das ganze ist automatisch erstellt worden und es kann wenig Einfluss darauf genommen werden wie die Darstellung aussieht. Je nach dem welche Methoden und Metriken ausgewählt werden werden kommen allerdings kleinere Abweichungen und etwas andere Darstellungen zustande.  
Ich habe mir verschiedene angeschaut und dann objektiv das ausgewählt, was anschaulich am besten die Parteien und Thesen gruppiert und sich damit am besten eignet. Ausgewählt habe ich hier Average Linking mit Euklidischem Abstand.

Die Verbindungen der einzelnen Cluster untereinander sind dann an den Linien, die aussehen wie ein Baum oder eine Wurzel, oben und links dargestellt.
Diese nennen sich Dendogramme und stellen dar wie die Thesen bzw. Parteien hierarchisch Gruppiert werden können. Es fängt also bei der kleinstmöglichen Gruppierung an und jede
Ebene in dem Baum stellt dann die nächstmögliche Gruppierung mit einer anderen Partei, These oder Gruppierung dar. Oben sind die Gruppierungen für die Parteien und links die Gruppierungen für die Thesen dargestellt

#### Analyse der Cluster

Das offensichtlichste an dieser Darstellung ist, dass die Partien ungefähr in ihre politischen Lager gruppiert werden. Die AfD und die NPD sind also sehr ähnlich zueinader und befinden sich zudem in einem Cluster mit der FDP, CDU, LKR und TIERSCHUTZ Hier! Das wäre also der rechte bzw. konservative Cluster.  
Der nächste Cluster bildet sich aus Die Humanisten, SPD, Die Partei, GRÜNE, Klimaliste ST und die Linke. Das sind offensichtlich Linke Parteien.
Interessanter wird es dann bei dem letzten Cluster aus WIR2020, DieBasis, PIRATEN, Tierschutzallianz, Tierschutzpartei, ÖDP und FREIE WÄHLER. Die bilden eine Mischung aus verschiedenem, wie z.B. Linksliberalismus, Grüner Politik und Wertkonservatismus. Oberflächlich betrachtet sind diese Parteien eher politisch in der Mitte anzufinden. Das spiegelt sich auch eher in dem Antwortverhalten wieder.  
Als letztes bleibt FBM übrig, über die ich wenig politische Informationen finde. Zumindest von dem Clustern und den Antworten betrachtet würde ich diese auch eher zentrisch einordnen, da diese Positionen von Linken sowie von Rechten vertreten.
Was durch diese Darstellung sehr gut sichtbar wird ist, welche Antworten auf welche Thesen einem bestimmten politischen Spektrum zugeordnet werden können.

### PCA Analyse

Ein etwas anderes Verfahren ist dann PCA, kurz für Principal Component Analysis und auf Deutsch Hauptkomponentenanalyse. Einfach gesagt versucht diese Methode eine Datenmenge in wenige Komponenten aufzuteilen, ohne das dabei die Bedeutung der Daten verloren geht. Hier wird dabei jeder These eine "Bedeutung" zugeteilt und daran kann erkannt werden inwiefern welche Thesen eher dafür verantwortlich sind, dass bestimmte Parteienspektren sich unterscheiden. Hier habe ich das mal für eine Komponente gemacht. Für zwei Komponenten wird das ganze schon wieder zu unübersichtlich.

<img src="https://user-images.githubusercontent.com/9419801/118012575-8335dc00-b351-11eb-8949-3692d9d85f99.png" alt="pca_1" width="300"/>

Thesen die hier sehr weit oben oder unten zu finden sind sorgen also eher dafür, dass durch diese die Parteien in verschiedene Cluster aufgeteilt werden können. In der Mitte befinden sich Thesen in denen sich viele Parteien eher einig sind. Als Beispiele kann These 1. genommen werden, für die fast alle Parteien mit "Ja" abgestimmt haben.
Wenn nun mehrere Komponenten miteinander analysiert werden dann kann ausgerechnet werden, inwiefern die Komponenten die Varianz in den Daten erklären können.



### Fazit
Die Cluster und die Nähe der Parteien sollten etwas kritisch betrachtet werden, weil die qualität der Thesen des Wahlomats oft keine gute Aufteilung der Parteien zulassen. 
Die Fragen stellen außerdem nur so etwas wie eine politische Stichprobe der Partien dar, also nur eine Abstraktion der Parteien auf 38 Fragen. Die tatsächlichen Wahlprogramme der Parteien sind sehr viel differenzierter und oft mehrere hundert Seiten lang. Wer also die wirklichen politischen Standpunkte der Parteien wissen will sollte sich die Wahlprogramme zumüte führen oder sich das Wahlverhalten der Fraktionen im Landtag oder Bundestag anschauen.
Ein anderes Problem sind die Antwortmöglichkeiten von Ja, Neutral, Nein. Ein besserer Überblick würde sicherlich erzielt werden wenn nicht nur schwarz und weiß entschieden werden könnte. Also in der Form von "Wie sehr Stimmen sie dieser These zu?" auf einer Skala von 1-5. So etwas wie die [Likert-Skala](https://de.wikipedia.org/wiki/Likert-Skala).

Letztendlich ist der Wahl-O-Mat nur ein Informationsangebot über Wahlen und Politik und soll keine Wahlempfehlung aussprechen.



