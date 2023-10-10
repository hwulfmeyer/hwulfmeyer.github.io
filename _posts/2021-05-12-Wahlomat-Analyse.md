---
title: "Analyse des Wahl-O-Mat für die Landtagswahl Sachsen-Anhalt 2021"
categories:
  - Blog
tags:
  - Wahlomat
  - Wahl-o-Mat
  - Landtagswahl
  - Wahlen
  - Visualisierung
  - Analyse
  - Daten
  - Clustering
  - Machine Learning
  - PCA
---

Dieses Jahr ist Wahljahr in der Bundesrepublik und so auch für den Landtag in Sachsen-Anhalt am 6. Juni.
Dafür wurde auch wieder ein [Wahl-O-Mat](https://www.wahl-o-mat.de/sachsenanhalt2021/app/main_app.html) veröffentlicht.

### Darstellung der Antworten
Die Antworten der Parteien können auf der Website ausgelesen werden und diese können dann hübsch visualisiert und mittels Clustering oder PCA sogar analysiert werden. Genau so wurde das schon von D. Kriesel zur letzten Bundestagswahl 2017 veröffentlicht. Siehe Teil 1 [hier](https://www.dkriesel.com/blog/2017/0903_auswertung_des_wahl-o-mats_zu_einer_parteienlandkarte) und Teil 2 [hier](https://www.dkriesel.com/blog/2017/0904_wahl-o-mat-auswertung_teil_2_thesen-_und_parteienverwandtschaften).
Ich habe mich von ihm inspirieren lassen und habe vor ein paar Wochen selbst damit begonnen so eine Analyse anzufertigen. Das Ergebnis habe ich ebenfalls in einer Clustermap dargestellt.

<img src="https://user-images.githubusercontent.com/9419801/118012930-df98fb80-b351-11eb-84a1-5940b64a0f70.png" alt="clustermap" width="600"/>
<sup>(Hinweis: Die Partei Gesundheitsforschung habe ich manuell entfernt, weil diese für alle Thesen "Neutral" als Antwort gegeben haben)</sup>

Die Spalten sind die Parteien und in den Zeilen befinden sich die Thesen und die Antworten der Parteien darauf.
Grün steht dabei für Zustimmung, Rot für Ablehnung einer These und Grau bzw. Weiß steht für Neutral. Die Thesen werden mit der offiziellen Kurzform des Wahl-O-Mats dargestellt.
Die kompletten Thesen mit einem Positionsvergleich findet ihr [hier](https://www.wahl-o-mat.de/sachsenanhalt2021/PositionsVergleichSachsenAnhalt2021.pdf). Die Kurzformen können manchmal etwas verwirrend sein. So ist z.B. These 10 die Frage nach einem Aufnahmestop für Flüchtlinge, wird aber hier mit "Aufnahme von Flüchtlingen" abgekürzt. 

Grob gesagt sind die Parteien ihrer Ähnlichkeit nach geordnet, also wie ähnlich sind die Antworten einer Partei zu einer anderen. Das Ganze basiert auf einem Clustering Verfahren, das sich [hierarchical/agglomerative clustering](https://de.wikipedia.org/wiki/Hierarchische_Clusteranalyse) nennt und versucht die Parteien und Thesen zu gruppieren. Das Verfahren benutzt eine Distanzmetrik wie zum Beispiel den Euklidischen Abstand. Jede These wird dabei als eine Dimension betrachtet und die Antwortmöglichkeiten dann als der Wertebereich (-1,0,1) den diese annehmen können.  
Normalerweise würden für n Parteien dann n<sup>(1-n)</sup> verschiedene Distanzen herauskommen, also jede Partei zu jeder anderen und um das verwertbar darstellen zu können wird dann Clustering verwendet. Die Grafik ist automatisch erstellt worden und es kann wenig Einfluss darauf genommen werden wie die Darstellung aussieht. Je nach dem welche Methoden und Metriken ausgewählt werden, kommen allerdings kleinere Abweichungen und etwas andere Darstellungen zustande. Aus den verschiedenen Darstellung habe ich eine ausgewählt, die die Parteien und Thesen am besten gruppiert.

Die Verbindungen der einzelnen Cluster untereinander sind dann an den Linien, die aussehen wie ein Baum oder eine Wurzel, oben und links dargestellt.
Diese nennen sich Dendrogramme und stellen dar wie die Thesen bzw. Parteien hierarchisch gruppiert werden können. Es fängt also bei der kleinstmöglichen Gruppierung an und jede
Ebene in dem Baum stellt dann die nächstmögliche Gruppierung mit einer anderen Partei, These oder Gruppierung dar. Oben sind die Gruppierungen für die Parteien und links die Gruppierungen für die Thesen dargestellt

#### Analyse der Cluster

Das Offensichtlichste an dieser Darstellung ist, dass die Parteien ungefähr in ihre politischen Lager gruppiert werden. Die AfD und die NPD sind also sehr ähnlich zueinander und befinden sich zudem in einem Cluster mit der FDP, CDU, LKR und TIERSCHUTZ Hier! Der Cluster besteht aus konservativen und wirtschaftsliberalen Parteien.
Der nächste Cluster bildet sich aus Die Humanisten, SPD, Die Partei, GRÜNE, Klimaliste ST und die Linke. Das sind die linken/linksliberalen Parteien.  
Interessanter ist der letzte Cluster aus WIR2020, DieBasis, PIRATEN, Tierschutzallianz, Tierschutzpartei, ÖDP und FREIE WÄHLER. Diese Parteien bilden eine Mischung aus verschiedenen politischen Ansichten wie z.B. Linksliberalismus, Grüner Politik und Wertkonservatismus. Oberflächlich betrachtet könnten man diese eher politisch der Mitte zuordnen. Das spiegelt sich auch in dem Antwortverhalten wieder, das linke sowie konservative Themen beinhaltet. Aus dem Dendrogramm ist allerdings auch ersichtlich, dass sich dieser Cluster näher an dem linken Spektrum befindet.  
Die Partei FBM wurde als einzige keinem größerem Cluster zugeordnet. Erst später in der Hierarchie wird die Partei zu dem großen Cluster der linken und zentrischen Parteien zugeordnet. FBM könnte deshalb wohl auch eher mitte-links eingeordnet werden.

Neben den Clustern für die Parteien existieren auch Cluster für die Thesen. Interessant ist hier, dass bestimmte Antworten auf Themen zusammengehörig zugeordnet werden können. Die oberen Themen werden also eher von konservativen Parteien bejaht, für mittleren Thesen herrscht eher ein Konsenz, während die unteren Thesen eher von linken Parteien bejaht werden.

### PCA Analyse

Um herauszufinden bei welchen Thesen eher Uneinigkeit besteht und damit eine bessere Unterscheidung der Parteien bezweckt wird, kann eine Principal Component Analysis (PCA) oder auf deutsch Hauptkomponentenanalyse benutzt werden. Diese Methode versucht eine Datenmenge in wenige Komponenten (Linearkombinationen) aufzuteilen, ohne das dabei die Signifikanz der Daten verloren geht. Jeder These wird dabei ein Dezimalwert zugeteilt. Das ganze ist ein Spektrum ins Negative und Positive und die Extremwerte sind eher von hoher Bedeutung. Hier habe ich das für eine Komponente ausgewertet wodurch eine Eindimensionale-Skala erstellt werden kann. Für mehr als eine Komponente wird die Darstellung zu unübersichtlich.

<img src="https://user-images.githubusercontent.com/9419801/118012575-8335dc00-b351-11eb-8949-3692d9d85f99.png" alt="pca_1" width="300"/>

Thesen die hier sehr weit oben oder unten zu finden sind sorgen eher dafür, dass durch diese die Unterschiede in den Parteien gut beschrieben werden können. In der Mitte (die grünlich gefärbten) befinden sich Thesen in denen sich viele Parteien eher einig sind. Zum Beispiel haben fast alle Parteien These 1 mit "Ja" beantwortet.  
Wenn nun mehrere Komponenten miteinander analysiert werden dann ist es möglich auszurechnen wie sehr die Komponenten die Varianz in den Daten erklären können. Dies wiederum einzeln und in Kombination miteinander (kumulativ).

<img src="https://user-images.githubusercontent.com/9419801/118014592-abbed580-b353-11eb-9bc3-3acd514985d5.png" alt="pca_variance" width="300"/>

Mit der ersten Komponenten kann also schon ca. 32% der Varianz der Daten erklärt werden. Mit diesen Ergebnissen können Rückschlüsse auf die Qualität der Fragen geworfen werden, oder auch auf die Komplexität der politischen Standpunkte in der deutschen Politik.

### Fazit
Die Cluster und die Nähe der Parteien sollten etwas kritisch betrachtet werden, weil die Qualität der Thesen des Wahl-O-Mats oft keine differenzierte Aufteilung der Parteien zulässt. 
Die Fragen können außerdem als politische Stichprobe der Parteien aufgefasst werden und stellen die Ansichten der Parteien nur abstrakt auf 38 Fragen dar. Die tatsächlichen Wahlprogramme der Parteien sind sehr viel differenzierter und oft mehrere hundert Seiten lang. Wer also die wirklichen politischen Standpunkte der Parteien wissen will, sollte sich die Wahlprogramme zu Gemüte führen, sich die Begründungen auf die Antworten im Wahl-O-Mat durchlesen oder sich das Wahlverhalten der Fraktionen im Landtag oder Bundestag anschauen.
Ein anderes Problem sind die Antwortmöglichkeiten von "Ja", "Neutral", "Nein". Ein besserer Überblick würde erzielt werden wenn die Antworten in Form des Grads der Zustimmung wären, z.B. so etwas wie die [Likert-Skala](https://de.wikipedia.org/wiki/Likert-Skala).

Letztendlich muss berücksichtigt werden, dass der Wahl-O-Mat nur ein Informationsangebot über Wahlen und Politik ist und keine Wahlempfehlung aussprechen soll.



