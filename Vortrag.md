<!--

author:   Jihad Hyadi

email:    Jihad.Hyadi@student.tu-freiberg.de

version:  0.0.1

language: de

comment:  Vortrag über die in der Bachelorarbeit geleistete Arbeit und die erreichten Ziele

icon:     https://upload.wikimedia.org/wikipedia/commons/d/de/Logo_TU_Bergakademie_Freiberg.svg

link:     ./styles.css

-->

[![LiaScript](https://raw.githubusercontent.com/LiaScript/LiaScript/master/badges/course.svg)](https://liascript.github.io/course/?https://raw.githubusercontent.com/jh-488/Vortrag-BA/main/Vortrag.md)

# Verbesserung des Lernens in Remote Laboren durch Anwendung von Gamification Ansätzen

| Thema             | Info                                                            |
| ----------------- | --------------------------------------------------------------- |
| **Veranstaltung** | `Vortrag zur Erlangung des Bachelors in angewandter Informatik` |
| **Semester**      | `Sommersemester 2024`                                           |
| **Hochschule**    | `Technische Universität Bergakademie Freiberg`                  |
| **Autor**         | `Jihad Hyadi`                                                   |
| **Betreuer**      | `Prof. Dr. Sebastian Zug, Dr. André Dietrich`                   |


# Einleitung

<!-- style="font-size: 2rem;"-->
* **Hintergrund und Kontext**

  <!-- style="font-size: 1.5rem;"-->
  - Der Einsatz von Remote Laboren in der Ausbildung hat stark zugenommen[4]
  - Edrys, eine Plattform für Remote-Laboren, bietet Studierenden die Möglichkeit, Mikrocontroller aus der Ferne zu steuern und zu programmieren
  - Gamification ist weithin als erfolgreiche Strategie zur Förderung des Engagements und der Beteiligung[6]

<!-- style="font-size: 2rem;"-->
* **Problemdarstellung**

  <!-- style="font-size: 1.5rem;"-->
  - Abwesenheit von physischem Kontakt oder direkter Manipulation der Hardware 
  - Traditionelle Aufgaben von Remote Laboren vermissen Aspekte der Motivation und Interaktion
  - Fehlen von sofortigem Feedback


**=> Integration von Gamification-Konzepten in Edrys, um die Motivation und Beteiligung der Studenten zu erhöhen**


## Ziele

* Entwicklung von Gamified-Aufgaben
* Förderung des studentischen Engagements
* Verbesserung der Lernergebnisse
* Bereitstellung unmittelbares Feedback
* Bewertung von Benutzerfreundlichkeit und Benutzererfahrung
* Sicherstellung von Skalierbarkeit und Flexibilität

<div class="flex">
    <img src="./images/remote_lab_eg.jpg" alt="Remote Lab Example"/>
    <figcaption>Remote Labor Bild[1]</figcaption>
</div>


# Agenda

<!-- style="font-size: 2rem; font-weight: 200;"-->
1. Einleitung
<!-- style="font-size: 2.5rem; font-weight: 600;"-->
2. Verwandte Arbeiten
3. Methodik und Implementierung
4. Ergebnisse
5. Fazit


# Verwandte Arbeiten

<div class="flex">
    <img src="./images/related_work.webp" alt="Related Work Image"/>
    <figcaption>Verwandte Arbeit Bild[2]</figcaption>
</div>

## Remote Laboren Projekte

~~Project MICRO~~
--------------------

- MICRO, The Remote Microprocessor Lab
- entwickelt von Studierenden der Informatik, Ingenieurinformatik und Elektrotechnik an der Technischen Hochschule Mittelhessen in Gießen
- Fernzugriff auf mehrere Labore durch Verbindung mit einer virtuellen Maschine
- MICRO-Cube setup

<div class="flex mbottom">
    <img class="border" style="width: 350px" src="./images/micro_cube.png" alt="Micro Cube Prototype"/>
    <figcaption>Prototyp eines MICRO Cube[3]</figcaption>
</div>

-> **Fehlen eines automatischen Einreichungssystems**

<!-- --{{1}}--
das eine direkte Bewertung der von den Studierenden eingereichten Arbeiten und eine sofortige Rückmeldung ermöglicht 
-->

~~Edrys~~
--------------------

- Einfache Einrichtung und gemeinsame Nutzung von Remote Laboren
- Klassenbildung durch Kombination von Modulen
- Einfache Echtzeit-API zur Erstellung von Modulen (Edrys.js API)

<div class="flex mbottom">
    <img class="border" style="height: 300px" src="./images/edrys_arduino_lab.png" alt="Edrys Arduino Lab"/>
    <figcaption>Beispiel für eine Edrys-Einrichtung[4]</figcaption>
</div>

-> **Aufrechterhaltung eines hohen Engagements und Motivation der Studenten**


## Gamified Remote Laboren Projekte

* ~~RALfie Project~~
--------------------

- The Remote Access Labs for Fun, Innovation and Education
- 2013, an der University of Southern Queensland in Australien 
- Steigerung des Engagements junger Lernender in den MINT-Fächern
- Gamifizierte Elemente: Punkte, Stufen und Abzeichen

<div class="flex">
    <img style="width: 400px" src="./images/ralfie_ui.png" alt="Ralfie UI"/>
    <figcaption>RALfie Benutzeroberfläche[5]</figcaption>
</div>

-> **einige Lernende hatten Schwierigkeiten, die Plattform zu nutzen, da der Inhalt nicht einfach zu verstehen war.**

* ~~Gamified Remote Labs for Engineering Students~~
--------------------

- 2021, während der Zeit der Covid-19-Pandemie, von Forschern der Universität Loughborough im United Kingdom
- eine Reihe von virtuellen Experimenten für Maschinenbaustudenten
- Die Übungen wurden in aufsteigender Reihenfolge der Schwierigkeit eingesetzt

-> **Verwendung von Fragen unterschiedlicher Art**


# Methodik und Implementierung

<div class="flex mtop">
    <img src="./images/implementation_icon.jpg" alt="Implementation Icon"/>
    <figcaption>Implementierung-Symbol</figcaption>
</div>

## Zentraler Server

* Entwicklung eines Servers, der sowohl unter Linux als auch unter Windows funktioniert
* Ermöglichung von Code-Tests für Feedback
* Entwicklung mit Node js

<div class="flex mbottom">
    <img src="./images/server_implementation.png" alt="Server Implementation"/>
    <figcaption>Upload-Prozess</figcaption>
</div>

**--> Starten des Servers:**

node index.js --core "CORE_NAME" --port "PORT_NAME"

(node index.js --core arduino:avr:uno --port COM3)


### Hochladen von Code

```javascript Eine Funktion zum Kompilieren eines Arduino-Sketches
compileSketch = (sketchPath) => {
    return new Promise((resolve, reject) => {
      const args = ["compile", "--log-level", "error", sketchPath, "-b", BOARD_CORE];
      const compileProcess = spawn("arduino-cli", args);
  
      // Listen for messages and errors in the compilation process
      let stdoutData = ""; 
      let stderrData = ""; 
  
      compileProcess.stdout.on("data", (data) => {
        stdoutData += data.toString(); 
      });
  
      compileProcess.stderr.on("data", (data) => {
        stderrData += data.toString();
      });
  
      // Listen for the completion of the compilation process
      compileProcess.on("close", (code) => {
        if (code === 0) {
          resolve({ message: "Compilation successful!", stdout: stdoutData });
        } else {
          reject({ message: `Compilation failed with code: ${code}`, stderr: stderrData });
        }
      });
    });
};
```

```javascript Eine Funktion zum Hochladen eines Arduino-Sketches auf ein Board
uploadSketch = (port, sketchPath) => {
  return new Promise((resolve, reject) => {
    const args = ["upload", sketchPath, "-p", port, "-b", BOARD_CORE]; 
    const uploadProcess = spawn("arduino-cli", args);

    // Listen for messages and errors in the upload process
    let stdoutData = ""; 
    let stderrData = ""; 

    uploadProcess.stdout.on("data", (data) => {
      stdoutData += data.toString(); 
    });

    uploadProcess.stderr.on("data", (data) => {
      stderrData += data.toString();
    });

    // Listen for the completion of the upload process
    uploadProcess.on("close", (code) => {
      if (code === 0) {
        resolve({ message: "Upload successful!", stdout: stdoutData });
      } else {
        reject({ message: `Upload failed with code: ${code}`, stderr: stderrData });
      }
    });
  });
};
```


### Unit Testing für Feedback

<div class="flex mbottom">
    <img src="./images/server_tests_imp.png" alt="Server Internal Process"/>
    <figcaption>Server Interner Prozess</figcaption>
</div>


**Beispiel:**

~~1. Schritt~~

```c Ein Sketch zum Einschalten der eingebauten LED
void setup () {
  pinMode(LED_BUILTIN, OUTPUT);
}

void loop () {
  digitalWrite(LED_BUILTIN, HIGH);
}
```

~~2. Schritt~~

<!-- data-marker="
0 0 0 100 rgba(55,255,100,0.5) text;
4 0 4 200 rgba(55,255,100,0.5) text;
9 0 9 300 rgba(55,255,100,0.5) text;
12 0 15 100 rgba(55,255,100,0.5) text"
data-showGutter="true"
-->
```c Ein Test-Sketch für die Turn On LED Aufgabe
#include <ArduinoUnit.h>

void setup () {
  pinMode(LED_BUILTIN, OUTPUT);
  Serial.begin(9600);
}

void loop () {
  digitalWrite(LED_BUILTIN, HIGH);
  Test::run();
}

test(turnOnLed){
  assertEqual(digitalRead(LED_BUILTIN), HIGH);
}
```

~~3. Schritt~~

``` Eine Testzusammenfassung für den Test
Test summary: 1 passed , 0 failed , 0 skipped , out of 1 test(s) .
```


## Module

* Ein Edrys-Modul ist eine Webseite, die mit HTML, CSS und JavaScript erstellt wird
* Einfache Integration in Edrys-Klassenräume
* Bewahrung einer benutzerfreundlichen Erfahrung

### Code Editor

<div class="flex mbottom">
    <img src="./images/code_editor.png" alt="Code Editor"/>
    <figcaption>Code Editor</figcaption>
</div>

```javascript Verbindung des Code Editors mit dem Server
// connect to the websocket server
var socket = new WebSocket(Edrys?.module?.serverURL || "ws://localhost:8080");

Edrys.onMessage(({ from, subject, body }) => {
  if (Edrys.role === "station") {
    // send the code and the challenge id through socket if connected
      if (!socket || socket.readyState !== WebSocket.OPEN) {
        Edrys.sendMessage('server-response', "Error: Server not connected!!");
      } else {
          socket.send(JSON.stringify({
            code: body,
            challengeId: Edrys.module.challengeId
          }));
        }
    }
  })
```

### Timer

<div class="flex mbottom">
    <img src="./images/timer.png" alt="Timer Module"/>
    <figcaption>Timer-Modul</figcaption>
</div>

```javascript Behandlung der vom Code-Editor empfangenen Nachrichten
Edrys.onMessage(({ from, subject, body, module }) => {
  if (subject === "challenge-solved") {
    // Calculate the time needed to solve the challenge
    elapsedTimeInSeconds = timerStart * 60 - time;
    const minutes = Math.floor(elapsedTimeInSeconds / 60);
    const seconds = elapsedTimeInSeconds % 60;

    stopTimer();

    feedbackContainer.classList.add("green-bg");
    setFeedbackMessage(
      minutes > 0
        ? `Congrats! Challenge solved in ${minutes} minutes and ${seconds} seconds!`
        : `Congrats! Challenge solved in ${seconds} seconds!`
    );
  } else if (subject === "pause-timer") {
    pauseTimer();
  } else if (subject === "continue-timer") {
    continueTimer();
  }
}, (promiscuous = true));
```

### Multiplayer Tab

<div class="flex mbottom">
    <img src="./images/multi0.png" alt="Multiplayer Tab"/>
    <figcaption>Multiplayer Tab Modul</figcaption>
</div>

```javascript Eine Funktion zur Aktualisierung der Spieler im Raum
const updatePlayersInRoom = () => {
  joinedPlayers.innerHTML = "";

  const allUsers = Edrys.liveClass.users;
  for (const idx in allUsers) {
    const user = allUsers[idx];

    if (user.room.includes("Station") && !user.displayName.includes("Station") && !usersInStation.includes(user.displayName)) {
      usersInStation.push(user.displayName);
    }
  }

  playersJoinedNumber = usersInStation.length;

  if (playersJoinedNumber >= 0) {
    for (const user of usersInStation) {
      joinedPlayers.innerHTML +=
        user === Edrys.liveUser.displayName
          ? `<div class='main_user'>${user} (Me)</div>`
          : `<div class='user_raw'>${user}</div>`;
    }
  } else {
    joinedPlayers.innerHTML = "<div>No players in room</div>";
  }

  // Enable start game button if all players have joined
  if (playersNumber === playersJoinedNumber) {
    startGameButton.disabled = false;
    spinner.style.display = "none";
  }
};
```

<div class="flex">
    <img src="./images/multi2.png" alt="Multiplayer Tab"/>
    <figcaption>Multiplayer Tab Modul (Spielbereich)</figcaption>
</div>


## Gamifizierte Aufgaben

* 4 verschiedene Arten von Aufgaben
* Integration von Gamification-Elementen in die Edrys-Plattform 
* Verbesserung des studentischen Engagements und der Lernergebnisse

### Turn On LED

<div class="flex mbottom">
    <img src="./images/gifs/turnonled.gif" alt="Turn On LED"/>
    <figcaption>Turn On LED Lab</figcaption>
</div>

```javascript Code-Editor wartet auf Nachrichten
Edrys.onMessage(({ from, subject, body, module }) => {
    if (subject === "timer-started") {
        // change the editor to writable when the timer starts
        enableEditor();
    } else if (subject === "timer-ended") {
        // change the editor to read-only when the timer ends and reset starter code
        clearEditor();

        disableEditor();
    } 
}, (promiscuous = true));
```


### Missing LED

<div class="flex mbottom">
    <img src="./images/gifs/missingled.gif" alt="Missing LED"/>
    <figcaption>Missing LED Lab</figcaption>
</div>

```javascript Senden der Nachricht „randomize leds“ an den Server
// connect to the websocket server
var socket = new WebSocket(Edrys?.module?.serverURL || "ws://localhost:8080");

// send a message to the server to start the challenge
startChallenge.onclick = () => {
  Edrys.sendMessage("randomize-leds", "Randomize LEDs!");
};

Edrys.onMessage(({ from, subject, body }) => {
  switch (subject) {
    case "randomize-leds":
      if (Edrys.role === "station") {
        if (!socket || socket.readyState !== WebSocket.OPEN) {
          Edrys.sendMessage("server-not-connected", "Server not connected!");
        } else {
          socket.send(
            JSON.stringify({
              challengeId: "randomize-leds",
              code: "",
            })
          );
  
          Edrys.sendMessage("server-connected", "Server connected!");
        }
      };
      break;
});
```

```javascript Beispiel für die in der JSON-Datei gespeicherten Daten
{
  "turnedOnLEDs": [
    11 ,
    12
  ],
  "turnedOffLED": 13
}
```

### RGB LED

<div class="flex mbottom">
    <img src="./images/gifs/rgbled.gif" alt="RGB LED"/>
    <figcaption>RGB LED Lab</figcaption>
</div>

```javascript Eine Funktion, die einen Sketch erzeugt, um die RGB-LED-Farbe zu ändern
const finalCode = (chosenColor) => {
    const code = `
        int redPin= 12;
        int greenPin = 11;
        int  bluePin = 13;

        void setup() {
            pinMode(redPin,  OUTPUT);              
            pinMode(greenPin, OUTPUT);
            pinMode(bluePin, OUTPUT);
        }

        void  loop() {
            setColor( ${chosenColor.redValue}, ${chosenColor.greenValue}, ${chosenColor.blueValue}); 
        }

        void setColor(int redValue, int greenValue,  int blueValue) {
            analogWrite(redPin, redValue);
            analogWrite(greenPin,  greenValue);
            analogWrite(bluePin, blueValue);
        }
    `

    return code
};
```


### Snake Game

<div class="flex mbottom">
    <img src="./images/gifs/snakegame.gif" alt="Snake Game"/>
    <figcaption>Snake Game Lab (Multiplayer)</figcaption>
</div>

```c Eine Funktion zur Anzeige eines fröhlichen Gesichts auf der LED-Matrix
void displayHappyFace() {
  reset();

  byte hf[8]= {B00111100,B01000010,B10100101,B10000001,B10100101,B10011001,B01000010,B00111100};

  lc.setRow(0,0,hf[0]);
  lc.setRow(0,1,hf[1]);
  lc.setRow(0,2,hf[2]);
  lc.setRow(0,3,hf[3]);
  lc.setRow(0,4,hf[4]);
  lc.setRow(0,5,hf[5]);
  lc.setRow(0,6,hf[6]);
  lc.setRow(0,7,hf[7]);
  delay(1000);
}
```

```c Eine Funktion zur Anzeige eines traurigen Gesichts auf der LED-Matrix
void displaySadFace() {
  reset();

  byte sf[8]= {B00111100,B01000010,B10100101,B10000001,B10011001,B10100101,B01000010,B00111100};

  lc.setRow(0,0,sf[0]);
  lc.setRow(0,1,sf[1]);
  lc.setRow(0,2,sf[2]);
  lc.setRow(0,3,sf[3]);
  lc.setRow(0,4,sf[4]);
  lc.setRow(0,5,sf[5]);
  lc.setRow(0,6,sf[6]);
  lc.setRow(0,7,sf[7]);
  delay(1000);
}
```


## Integration mit Edrys

* Erstellung einer Konfigurationsdatei (.yml) für jedes Labor
* Die Modulkonfiguration besteht aus verschiedenen Eigenschaften, die vom Modul zur Ausführung bestimmter Aufgaben verwendet werden können

```yml Ein Beispiel für die Konfiguration des Code-Editors
- url: https://jh-488.github.io/Edrys_Code_Editor/index.html
    config:
      editorText: |
        void setup() {

        }

        void loop() {

        }
      runCommand: execute
      language: cpp
    showInCustom: station
    width: full
    height: huge
    serverURL: ws://localhost:8080
    challengeId: turn-on-led-001
    challengeType: time-restricted
```

```javascript Deaktivierung des Code-Editors, wenn die Aufgabe zeitlich begrenzt ist
Edrys.onReady (() = > {
  if (Edrys.module.challengeType === "time-restricted") {
    disableEditor();
  }
})
```



# Ergebnisse

<div class="flex mtop">
    <img src="./images/results_icon.png" alt="Results Icon"/>
    <figcaption>Ergebnisse-Symbol</figcaption>
</div>

## Bewertung der Leistung

+ **Unit Tests:**

  + Methode zum Testen kleiner Codestücke (Funktionen...)

  + Frühzeitiges Erkennen und Isolieren von Fehlern

  + Jest

```javascript Ein Beispiel für einen Unit-Test mit Jest
test("changeTab hides and shows containers correctly", () => {
    const showContainers = [document.createElement("div")];
    const hideContainers = [document.createElement("div")];
    const displayStyle = "flex";

    // Simulate initial state 
    showContainers[0].style.display = "none";
    hideContainers[0].style.display = "block";

    changeTab(showContainers, hideContainers, displayStyle);

    expect(showContainers[0].style.display).toBe(displayStyle);
    expect(hideContainers[0].style.display).toBe("none");
});
```

<div class="flex mbottom">
    <img style="width: 700px" src="./images/timer_test.png" alt="Test summary for the Timer Module"/>
    <figcaption>Testzusammenfassung für das Timer-Modul</figcaption>
</div>

<div class="flex mbottom">
    <img style="width: 700px" src="./images/multi_test.png" alt="Test summary for the Multiplayer Tab Module"/>
    <figcaption>Testzusammenfassung für das Multiplayer-Tab-Modul</figcaption>
</div>


+ **Integrationstests:**

  + Zu testen, wie die verschiedenen Komponenten miteinander funktionieren

  + Identifizierung der Konflikte zwischen den Elementen 

  + Bewertung der verschiedenen möglichen Szenarien



## Engagement und Feedback der Nutzer

<div class="flex mbottom">
    <img src="./images/survey_setup.jpg" alt="Setup of the survey labs"/>
    <figcaption>Einrichtung der Umfragelabore</figcaption>
</div>


<div class="flex mbottom">
    <img class="border" src="./images/edrys_survey/skill_lvl.png" alt="Arduino programming level of the students"/>
    <figcaption>Arduino-Programmierkenntnisse der Studenten</figcaption>
</div>


<div class="flex mbottom">
    <img class="border" src="./images/edrys_survey/how_fun.png" alt="Diagram to illustrate how enjoyable were the labs"/>
    <figcaption>Diagramm zur Veranschaulichung, wie unterhaltsam die Labore waren (1: „So viel Spaß“, 5: „Langweilig“)</figcaption>
</div>


<div class="flex mbottom">
    <img class="border" src="./images/edrys_survey/best_one.png" alt="A comparison of the different challenges"/>
    <figcaption>Ein Vergleich der verschiedenen Aufgaben</figcaption>
</div>


--> **Vorschlag**: die Spieler können gleichzeitig mit der Lösung der Aufgabe beginnen, so dass ein Spieler nicht warten muss, bis er an der Reihe ist.


## Auswertung der Ergebnisse

* Positives Feedback von den Studenten
* Effektive Motivation der Studenten durch die Gamification-Elemente wie einen Timer, einen Multiplayer-Modus und interaktives Feedback 
* Ausgangspunkt für die Entwicklung und den Einsatz von Gamification-Konzepten für Remote Labs in eingebetteten Systemen 

**--> Das am meisten geschätzte Konzept war die sofortige Rückmeldung der Antworten an die Benutzer.**

> “Die automatisierten Tests zeigen am Ende Erfolg oder Misserfolg.”
>
> “Sie erhalten eine direkte visuelle Rückmeldung darüber, ob etwas richtig oder falsch ist.”
>
> “Sie erhalten schnelles Feedback für den Code an einem realen Beispiel. Das Programmieren fühlt sich realer und sinnvoller an.”
>
> -- Antworten der Studenten auf die Frage, welches Element ihnen am besten gefallen hat



# Fazit

<div class="flex">
    <img src="./images/conclusion_icon.png" alt="Conclusion Icon"/>
    <figcaption>Fazit-Symbol</figcaption>
</div>

## Erreichung der Ziele

+ **Förderung des Engagements von Studenten**

  + Gestaltung interaktiver Aufgaben, gekoppelt mit einem unmittelbaren Feedback-Mechanismus 

  + Erzielung einer angenehmeren und dynamischeren Atmosphäre

  + Unterstützung der Lernenden beim Erkennen ihrer Fehler durch sofortiges Feedback

+ **Demonstration der Wirksamkeit von Gamification**

  + Die Studierenden fanden die spielerischen Übungen im Vergleich zu traditionellen Lernmethoden angenehmer und ansprechender

  + Der gamifizierte Ansatz ist sowohl unterhaltsam als auch lehrreich

+ **Bereitstellung eines funktionalen und zuverlässigen Systems**

  + Bereitstellung einer freundlichen Benutzererfahrung

  + Die entwickelten Komponenten können leicht integriert oder weiterentwickelt werden


## Herausforderungen

<!-- style="font-size: 2rem;"-->
* Aufgaben Design
* Feedback in Echtzeit
* Server-Leistung
* Entwicklung gamifizierter Elemente


## Beschränkungen und zukünftige Arbeiten

+ **Stichprobengröße und Vielfalt der an der Umfrage teilnehmenden Studenten**

  + Die aktuelle Studie basiert auf einer relativ kleinen Gruppe von Teilnehmern

  + Die Ergebnisse konnten nicht verallgemeinert werden

  --> Künftige Studien sollten sich an größere und vielfältige Gruppen richten, die mehr Tester mit unterschiedlichem Hintergrund, Programmierkenntnissen und akademischem Niveau umfassen.

+ **Entwurf und Entwicklung von kollaborativen Aufgaben**

  + Lernenden können in einem Team arbeiten, um ein Problem zu lösen

+ **Hinzufügung eines Backend-Servers, der mit einer Datenbank verbunden ist**

  + Verbesserung der Entwicklung von Modulen

  + Einführung neuer Konzepte (Benutzerprofilseite...)

  + Integration eines Punktesystems (Punkte, Abzeichen, Bestenlisten...)




# ‎ 

<div class="flex">
    <img style="width: 800px" src="./images/gifs/turnonled_multi.gif" alt="Turn On LED Lab in Multiplayer Mode"/>
    <figcaption>Turn On LED im Multiplayer-Modus</figcaption>
</div>



# Quellenangaben

* [1] https://www.nsta.org/science-teacher/science-teacher-julyaugust-2021-0/remote-labs-20-rescue
* [2] https://www.seattletimes.com/explore/careers/knowing-when-and-how-to-compromise-at-work/
* [3] Micro: The remote microprocessor lab.  https://doi.org/10.33968/2023.36
* [4] Adaptable digital labs - motivation and vision of the crosslab project, p. https://ieeexplore.ieee.org/document/9942759
* [5] Using gamification to create opportunities for engagement, collaboration and communication in a peer-to-peer environment for making and using remote access labs. https://ieeexplore.ieee.org/document/7463271
* [6] Using game design elements in non-gaming contexts.  https://doi.org/10.1145/1979742.1979575





# Zusätzliche Folien

## Systemarchitektur

+ **Präsentationsschicht:** 

  + Benutzeroberfläche, mit der die Studenten interagieren

  + Edrys modules

  + HTML, CSS, JavaScript

+ **Anwendungsschicht:**

  + Kernfunktionalitäten des Systems

  + Verbindung zwischen mehreren Modulen

  + Bearbeitung von Benutzeranfragen in der Server 

+ **Datenschicht:**
  
  + Unterschicht der Präsentations- und Anwendungsschicht

  + Nutzer können Daten wie die für die Lösung einer Aufgabe benötigte Zeit oder Feedback einsehen

  + Ein Sketch, das auf das Board hochgeladen werden muss, wird auf dem Server gespeichert 


## Hauptbestandteile

Zentraler Server:
================

* Entwicklung eines Servers, der sowohl unter Linux als auch unter Windows funktioniert
* Ermöglichung von Code-Tests für Feedback
* Entwicklung mit Node js

**--> Eine schnelle Alternative, um Code von Edrys zu empfangen und auf das Board zu laden**

Module:
================

* Code editor
* Timer
* Multiplayer Tab

**--> Bereitstellung einer ansprechenden Erfahrung für Remote-Laboren**

Gamifizierte Aufgaben:
================

| Name          | Schwierigkeitsgrad |  Erforderliche Module                        | Erforderliche Hardware                                        | 
| ------------- | :----------------: | :------------------------------------------: | :-----------------------------------------------------------: |
| Turn On LED   | leicht             | Code Editor, Timer, Video Stream             | Arduino Uno                                                   |
| Missing LED   | mittelschwierig    | Code Editor, Missing LED Modul, Video Stream | Arduino Uno, Breadboard, 3 LEDS, 3 Resistors, 4 Jumper Wires  |
| RGB LED       | leicht             | RGB LED Modul, Video Stream                  | Arduino Uno, Breadboard, RGB LED, 3 Resistors, 4 Jumper Wires |
| Snake Game    | schwierig          | Code Editor, Video Stream                    | Arduino Uno, 8x8 LED Matrix, 5 Jumper Wires                   |

**--> Umsetzung verschiedener Ansätze, um herauszufinden, welcher am besten geeignet ist, das Engagement der Lernenden aufrechtzuerhalten**