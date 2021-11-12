---
title: "Ein automatisierter Melder für Impftermine in Magdeburg"
categories:
  - Blog
tags:
  - Impfen
  - Impfung
  - Melder
  - Corona
  - Covid
  - Covid19
  - Magdeburg
  - python
  - telegram
  - raspberrypi
  - raspberry
  - pi
---

Anfang dieses Jahres startete die große Impfkampagne gegen Corona in Deutschland. Ich machte mir zu dem Zeitpunkt noch keinen großen Kopf über das Impfen, 
weil es zu der Zeit nur für die ältere Bevölkerung (70+) freigeben war. Im Frühjahr 2021 kam ich der ganzen Materie näher,
als sich meine nähere Familie die älter als 60 waren oder Vorerkrankungen besaßen auch Impfen lassen konnte. Die Terminbuchung erfolgte über eine sehr simple
Website mit einem Buchungssystem. Hier ein paar Impressionen davon:


<img src="https://user-images.githubusercontent.com/9419801/141386628-a5322d8c-e943-4bb0-a77d-5f0dae5ee652.PNG" alt="buchen" width="300"/>

<img src="https://user-images.githubusercontent.com/9419801/141386636-1d8e74ba-aa5c-4d7f-9f9c-e86227904558.PNG" alt="kalender" width="300"/>

Darüber erfuhr ich zirka im März 2021 in einem Telefonat mit meinem Vater, der mir berichtete, dass er immer Abends bis 24Uhr am Laptop saß und versuchte einen Termin zu ergattern.
Anders war das gar nicht möglich.
Die Termine waren rar und immer sehr schnell belegt. Man musste also entweder wissen, wann neue Termine online kamen oder Glück haben.
In diesem Moment kam mir der Gedanke,
dass das Ganze einfacher gehen müsste. Und somit machte ich mich an die Aufgabe dies herauszufinden. 

### Umsetzung

Eine einfache Analyse der Website mittels der [Firefox Tools für Webentwickler](https://developer.mozilla.org/de/docs/Tools) zeigte mir, 
dass die Betreiber des Dienstes eine relativ offene API benutzten. Über diese API konnte man auf alle nützlichen Daten zugreifen, freie Termine,
alle Daten der verfügbaren Termine und vieles mehr. Über sehr einfache HTTP requests konnte also herausgefunden werden ob gerade Termine frei sind.

Diese Information musste ich nur irgendwie an die Leute bringen. Ich dachte über eine Website mit [Web Push Notifications](https://support.mozilla.org/en-US/kb/push-notifications-firefox) nach.
Das erschien mir dann doch eher als unpraktikabel. Und so lenkte sich mein Blick richtung des Telegram Messengers. Telegram erfreute sich seit Anfang des Jahres
erhöhter Beliebtheit, weil Whatsapp die  [Nutzungsbedingungen geändert hatte](https://www.heise.de/news/WhatsApp-aendert-Nutzungsbedingungen-Daten-werden-mit-Facebook-geteilt-5005893.html), was dem Messenger erlaubte Daten mit Facebook zu teilen.
Außerdem hat Telegram eine Channelfunktion, in denen der Besitzer anonym Nachrichten verschicken kann und dies auch bequem von einem Bot übernommen werden lassen kann. Der Plan stand, jetzt fehlte nur noch die Umsetzung.

Ich entschied ich mich für Python, weil ich wusste, dass dort bereits alle Packages zur verfügung gestellt sind die ich für die Umsetzung brauchte.
Mit Python gestaltete sich die Programmierung außerdem als sehr einfach. An einem produktiven Abend und innerhalb weniger Stunden war ein automatisierter
Melder für Impftermine fertig.

Meldungen kommen dabei automatisiert in drei Fällen:
  - 12,5% Unterschied der freien Termine
  - Es gibt keine freien Termine mehr
  - Es gibt wieder freie Termine

Der interessierte Leser kann den Programmcode hier einsehen: https://github.com/hwulfmeyer/ImpfmelderMagdeburg/blob/master/impfungen.py

Und so sieht der Melder in der Praxis aus:

<img src="https://user-images.githubusercontent.com/9419801/141389485-8082f936-fa74-4bf9-9419-7130a2b2e39e.PNG" alt="impfmelder" width="300"/>

Das Programm musste ich natürlich auch irgendwo laufen lassen. Dafür eignete sich sehr gut einer der Raspberry PI 3 B+ bei mir Zuhause. 
Der Raspberry PI ist ein sehr kleiner Einplatinencomputer, der ungefähr die Größe eines Handys besitzt und alles an Hardware beinhaltet, was für einen Computer nötig ist.

<img src="https://user-images.githubusercontent.com/9419801/141391049-5278182d-0236-4ec4-94dd-7d275369b32a.png" alt="RASPBERRY_PI_3B_PLUS" width="300"/>

Über das dort aufgespielte
Linux System wird das Programm alle 5 min ausgeführt und eine Datei über den Stand der Impftermine auf der Festplatte gespeichert.
Ein paar updates später und ein stabiles System stand zur Verfügung, welches ich bis heute nicht ein einziges Mal warten musste.

### Statistiken

Den Impfmelder wollte ich intern erst einmal Testen, damit ich sicherstellen konnte, dass die Meldungen zuverlässig sind. Weil ich von der Buchungswebsite abhängig war, ging es auch nur darüber. Ich musste also warten, bis wieder Termine frei waren und das dauerte. Ein paar Tage und Tests später und der Melder konnte endlich frei zur Verfügung gestellt werden. Das war am 11. Mai. Über einen einfachen Link kann dem Channel beigetreten werden: https://t.me/MagdeburgImpfmelder

Den Einladungslink habe ich bekannten und Freunden geschickt und in größeren Gruppen in denen ich war geteilt. Über Mundpropaganda verbreitete sich das recht schnell, sodass immer mehr Nutzer dem Channel beitraten und sich schon bald exponentielles Wachstum einstellte.

Den Höhepunkt an Abonnenten erreichte der Channel am 11. Juni 2021 mit 1732 Nutzern.

<img src="https://user-images.githubusercontent.com/9419801/141390147-a31fa0b0-d6d7-45bf-a0f3-81c475ea9726.jpg" alt="statistik1" width="300"/>


Dabei wurden die Beiträge in dem Channel wohl bis zu 45.000 Mal angeschaut.

<img src="https://user-images.githubusercontent.com/9419801/141392949-42fad54e-41c0-42cb-9cd2-a29ed00da226.jpg" alt="statistik2" width="300"/>


Mittlerweile (12. November 2021) verzeichnet der Channel nur noch 1027 Nutzer.

<img src="https://user-images.githubusercontent.com/9419801/141390311-9f7bb94b-dd72-4c56-830b-8c193543b14f.jpg" alt="statistik3" width="300"/>

Beitritte verzeichnet der Channel auch nur noch kaum bis gar keine mehr.

<img src="https://user-images.githubusercontent.com/9419801/141391876-cecf337d-1c2d-47cd-b70b-15f1f2e218db.jpg" alt="statistik4" width="300"/>

Viele dieser Nutzer werden den Channel nicht mehr aktiv verfolgen und die Notification dafür deaktiviert haben.
Das spiegelt sich auch in der Aufrufstatistik oben wieder. 

