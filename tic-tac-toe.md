# Tic Tac Toe

Inspiriert von [Android App programmieren: TicTacToe (Anfänger)](https://www.youtube.com/watch?v=1lnxpZZw9hc)

Wir wollen ein Tic Tac Toe Spiel für Android programmieren.

![](images/tic-tac-toe-game.png)

## Das "Tic Tac Toe" Projekt generieren

Nach der Installation von Android Studio, klick auf _+Start a new Android project_
oder, wenn Android Studio bereits offen ist, führe _File > New > New Project_ aus.

Ein Dialog in zwei Schritte konfiguriert das Projekt:
- Die  "Empty Activity" auswählen und auf _Next_ klicken.
- "Tic Tac Toe" als _Name_ setzen.
- Sicherstellen, dass folgende Werte richtig gesetzt sind:
  - Die _Language_ ist "Kotlin"
  - Die _Minmum API Level_ ist "API 24: Android 7.0 (Nougat)"

Nachdem "Finish" geklickt wurde, generiert Android studio ein Neues Projekt. Zwei Dateien aus dem _app_ Ordner sind für uns besonderst wichtig:
- `activity_main.xml` (in _app > res > layout_) ist die Layout-Datei mit dem einem "Hellow World" text.
- `MainActivity.kt` (_app > java > com.example.tictactoe_) hat bereits den _Main_ "Entry point", mit dem nötigen Code, um das Layout zu laden.

## Das Layout gestalten

Zuerst kümmern wir uns um das Layout.

Wir möchten einen Statustext ganz oben und darunter eine Tabelle mit drei Spalten und drei Zeilen, in der die `X` und `0` gesetzt werden.

### Der Statustext

Für den Statustext können wir das "Hello World" Textfeld benutzen.

Auf "Hello World" klicken und in den _Attributes_ Panel folgende Werte setzen:

- _id_: `statusText`
- _text_: `X ist an der Reihe`
- Untere _Constraint_ im Layout entfernen  
  ![](images/tic-tac-toe-status-top.gif)

### Das Spielgitter

Für das Spielgitter benutzen wir eine Tabelle.

Zuerst können wir ein _Table Layout_ aus der linke Palette ziehen und unter den "X ist an der Reihe" Text plazieren.

![](images/tic-tac-toe-table-layout.gif)

Die Tabelle soll ein wenig Rand bekommen und quadratisch dargestellt werden.  

Per Mausklick die Tabelle aktivieren und in _Constraint Widget_-Panel diese Werte setzen:

- _Left Margin_ und _Right Margin_ sollen auf `8` gesetzt werden
- _Top Margin_ auf `24`.
- Eine "Top Constraint Layout" setzen.
- Das Breite/Höhe Verhältnis auf `1:1` setzen

![](images/tic-tac-toe-size-constraints.gif)

Für das Tic Tac Toe Spiel soll die Tabelle aus drei Zeilen und drei Spalten bestehen.  

Im _Component Tree_ Panel, das _TableLayout_ Element auswählen und:

- Die letzte Row entfernen.
- Die drei Rows markieren und in den _Attributes_ Panel, den _layout_weight_ auf `1` setzen.
- In der erste Zeile (Row), ein _TextView_-Feld aus der _Palette_ / _Text_ hinzufügen und sein _text_ auf `X` setzen
- Im _Component Tree_, das soeben kreierte Feld kopieren und zwei mal in der erste Zeile einfügen (`ctrl-c ctrl-v ctrl-v`...)
- Die _id_ auf `topLeftText`, `topCenterText` und `topRightText` setzen
- Im _Component Tree_ alle drei Text-Felder auswählen und in den _Attributes_:
  - _layout_height_ auf _match_parent_ setzen.
  - _textAppareance_ auf _Large_ setzen
  - Bei _gravity_, _center_ aktivieren
  - _layout_weight_ auf `1` setzen.
- ![](images/tic-tac-toe-columns.gif)
    - Im _Component Tree_
      - alle drei Text-Felder auswählen,
      - sie kopieren (`ctrl-c`)
      - und in den zwei weitere Zeilen einfügen (`ctrl-v`)
      - die _id_s umbenennen (`centerLeftText` bis `bottomRightText`)

Wir müssen noch die Linien zeichnen lassen indem wir ein Rahmen definieren.  
Leider haben die Tabellen keine Rahmen und wir müssen mit dem Hintegrund von der Tabelle und den Zellen _spielen_...  
Im _Component Tree_ TableView auswählen und in den _Attributes_ der Wert von _background_  auf `@android:color/black` setzen: Du kannst anfangen "black" ins Inputfeld zu schreiben, und Android Studio wird die _richtige_ Farbe vorschlagen (falls _background_ nicht sichtbar ist, kannst du ihn suchen...).

Dann müssen wir im _Component Tree_ alle neun Zellen auswählen (vor dem Klicken, die "Ctrl"-Taste drücken) und ihren _background_ auf `@android:color/white` setzen.

Wir brauchen noch die Ränder anzupassen:

- Für die drei Zellen in der mittleren Spalte, setzen wir den _Layout_marginLeft_ und _Layout_marginRight_ auf `1dp`
- Für die drei Zellen in der mittleren Zeile, setzen wir den _Layout_marginTop_ und _Layout_marginBottom_ auf `1dp`

Das Layout ist fertig: wir können noch den `X` im _text_ bei allen Zellen entfernen.

![](images/tic-tac-toe-layout.png)

Es ist nun Zeit zur `MainActivity.kt` zu wechseln und mit dem Programmieren anzufangen.

## Im Emulator die App ausführen

Während der Gestaltungphase konnten wir das Design in Android Studio sehen. Sobald wir Code in der App haben, brauchen wir den Emulator, damit unser Programm ausgeführt werden kann.

Falls kein Emulator bereits konfiguriert ist, kannst du darüber [lesen](emulator.md).

Das grüne Dreieck in der Toolbar ![](images/android-studio-run-app-start.png) startet den Emulator für das aktive Projekt.

## Die Logik programmieren

In `MainActivity.kt` wurde eine `MainActivity` Klasse mit der `onCreate()` Funktion für uns generiert. `onCreate()` hat auch bereits eine  Verbindung mit der Layout-Datei:

```kt
setContentView(R.layout.activity_main)
``` 

Unsere erste Programmieraufgabe ist es, ein `X` im oberen linken Feld erscheinen zu lassen, wenn wir darauf klicken. Dafür ergänzen wir die `onCreate()` Funktion mit unserem Code.

Wenn du vorhin im Layout für das erste Textfeld die _ID_ `topLeftText` gesetzt hast, kannst du nach der Zeile 11 eine neue Zeile hinzufügen und dort anfangen `top` zu schreiben. Android Studio sollte `topLeftText` vorschlagen: du kannst die Option mit der Eingabe-Taste bestätigen:

![](images/tic-tac-toe-code-top-left-variable.gif)

Damit hilft dir Android Studio nicht nur lange Namen zu tippen, sondern fügt auch auf Zeile 5 den `import` ein, wodurch alle Felder aus dem Layout nun auch im Code zu Verfügung stehen:

```kt
import kotlinx.android.synthetic.main.activity_main.*
```

Wenn du `topLeftText` ohne Hilfe von Android Studio getippt hast, musst du die `import` Zeile auch selbst hinzufügen.

Jedes Feld aus dem Layout hat eine leere `setOnClickListener` Funktion, die wir erweitern werden.

Hier hilft dir Android Studio wieder beim Tippen: statt `setOnClickListener` kannst du `socl` tippen (die ersten Buchstaben von "set on click listener"). Wähle aus den Vorschlägen die Version mit den geschleiften `{}` Klammern und Android Studio kümmert sich um den Rest:

![](images/tic-tac-toe-set-on-click-listener.gif)

Der Code ist ganz einfach: Wenn das Feld geglickt wird, setzten wir den `text` von `topLeftText` auf `X`:

```kt
override fun onCreate(savedInstanceState: Bundle?) {
    super.onCreate(savedInstanceState)
    setContentView(R.layout.activity_main)

    topLeftText.setOnClickListener {
        topLeftText.text = "X"
    }
}
```

Du kannst jetzt deinen Code im Emulator testen: Wenn du auf das oberste, linke Feld klickst, erscheint ein "X".

![](images/tic-tac-toe-click.gif)

Wenn der Emulator schon läuft, kannst du auf "'Run' App" ![](images/android-studio-run-app-restart.png) klicken, um die App wieder zu laden, ohne den ganzen Emulator neuzustarten.

Wir wollen den gleichen Click Listener für alle Textfelder definieren. Dafür definieren wir eine Liste von Felder und brauchen eine `For`-Schleife und den Empfänger (_Listener_) zu definieren:

Wir ersetzen

```kt
topLeftText.setOnClickListener {
    topLeftText.text = "X"
}
```

mit

```kt
val textFields = arrayOf(topLeftText, topCenterText, topRightText,
    centerLeftText, centerCenterText, centerRightText,
    bottomLeftText, bottomCenterText, bottomRightText)

for (textField in textFields) {
    textField.setOnClickListener {
        (it as TextView).text = "X"
    }
}
```

Wir haben vier Änderungen gemacht:

- zuerst haben wir  den `setOnClickListener` für `topLeftText` gelöscht.
- dann haben wir die neun Felder aus dem Layout in das Array `textFields` eingefügt,
- mit einer `for`-Schleife gehen wir duch alle `textField` in `TextFields` durch,
- wir setzen nicht mehr direkt das `X` im `text` vom `topLeftText`, sondern setzen es in den `it` Parameter, den `setOnClickListener` uns zu Verfügung stellt (du kannst ein Hinweis darauf neben der `{` sehen: `it:View!`)

Und schon können wir die Emulation starten und alle neun `X` setzen.

Aber es soll abwechslungsweise eine `X` und eine `0` geben! Wir definieren deshalb ein _Class field_ mit den Zeichen `X` oder `0`:

```kt
class MainActivity : AppCompatActivity() {

    private var currentSign = "X"

    override fun onCreate(savedInstanceState: Bundle?) {

        // ...

        for (textField in textFields) {
            textField.setOnClickListener {
                (it as TextView).text = currentSign
                currentSign = if (currentSign == "X") "0" else "X"
            }
        }
    }
}
```

Die wichtigen Änderungen sind:

- wir definieren `currentSign`, initialisiert auf `X`
- beim Klicken setzen wir den Text auf den Wert von `currentSign`...
- ... und wir setzen `currentSign` abwechslungsweise auf `X` und `0`

Und - funktioniert's in der Simulation?

Aber es gibt ein Problem: Wir können auf dem gleichen Feld zweimal klicken und das Zeichen ändern.  
Das sollte nicht sein:

```kt
textField.setOnClickListener { view ->
    view as TextView
    if (view.text == "") {
        view.text = currentSign
        currentSign = if (currentSign == "X") "0" else "X"
    }
}
```

- wir benennen den `it` parameter in `view` um und casten ihn zu eine `TextView`,
- bevor wir das Text-Feld setzen, prüfen wir, ob der Text noch leer ist.

Nun kann man nicht mehr auf ein besetztes Feld ein zweites Mal klicken, oder?

Es gibt noch einen Schönheitsfehler: In der App wird der Statustext nicht aktualisiert: Wir fügen diese Zeile am Ende der `if`-Bedingung hinzu:

```kt
statusText.text = "${currentSign} ist an der Reihe"
```

Fehlt noch was? Klar, wer hat nun gewonnen?

## Hat jemand gewonnen?

Um zu wissen, ob jemand gewonnen hat, muss das Programm prüfen, ob drei Nachbarfelder gleich sind.

Dafür fügen wir zur Klasse `MainActivity` die private Funktion `isWinner()` hinzu: nach dem Ende von `onCreate()`, aber vor der schliessenden geschleiften Klammer `}` der Klasse.

```kt
    private fun isWinner(): Boolean {
        return topLeftText.text == topCenterText && topCenterText == topRightText
    }
```

In einem ersten Schritt prüfen wir, ob die drei Felder in der erste Zeile gleich sind:
- `==` ist ein Vergleich (`=` ist eine Zuweisung: nicht genauch das Gleiche),
- und `&&` heisst "und".

Ist das genug? Nein, auch drei leere Felder wären gleich: Das müssen wir ausschliessen. Bevor wir die gleicheit prüfen, stellen wir sicher, dass das erste Feld nicht leer ist:

```kt
    fun isWinner(): Boolean {
        return topLeftText.text != "" && topLeftText.text == topCenterText.text && topCenterText.text == topRightText.text
    }
```

Kleiner Tipp: hast du gemerkt, dass du `tLT` tippen kannst, und Android Studio sofort `topLeftText` vorschlägt?

Bis jetzt prüfen wir nur die erste Zeile. Aber wir können bereits die `isWinner()` Prüfung im `setOnClickListener()` einfügen und dann testen, ob die App erkennt, dass jemand gewonnen hat:

```kt
if (view.text == "") {
    view.text = currentSign
    if (isWinner()) {
        statusText.text = "${currentSign} hat gewonnen"
    } else {
        currentSign = if (currentSign == "X") "0" else "X"
        statusText.text = "${currentSign} ist an der Reihe"
    }
}
```

Es geht weiter mit der zweiten Zeile:

```kt
private fun isWinner(): Boolean {
    return (topLeftText.text != "" && topLeftText.text == topCenterText.text && topCenterText.text == topRightText.text) ||
        (centerLeftText.text != "" && centerLeftText.text == centerCenterText.text && centerCenterText.text == centerRightText.text)
}
```

Die zwei Zeilen sind durch ein oder `||` verbunden: es reicht, dass eine von beide wahr ist.

... und die dritte:

```kt
    fun isWinner(): Boolean {
        return (topLeftText.text != "" && topLeftText.text == topCenterText.text && topCenterText.text == topRightText.text) ||
            (centerLeftText.text != "" && centerLeftText.text == centerCenterText.text && centerCenterText.text == centerRightText.text) ||
            (bottomLeftText.text != "" && bottomLeftText.text == bottomCenterText.text && bottomCenterText.text == bottomRightText.text)
    }
```

Wir wiederholten uns in der Gleichheitsprüfung stark. Die Wiederholungen wollen wir durch eine Funktion `areEqual()` ersetzen, damit der Code lesbarer wird. Wir fügen deshalb eine zweite Funktion hinzu:

```kt
private fun areEqual(a: TextView, b:TextView, c: TextView): Boolean {
    return a.text != "" && a.text == b.text && b.text == c.text
}
```

... und dann in `isWinner()` drei Mal verwenden.

```kt
private fun isWinner(): Boolean {
    return areEqual(topLeftText, topCenterText, topRightText) ||
            areEqual(centerLeftText, centerCenterText, centerRightText) ||
            areEqual(bottomLeftText, bottomCenterText, bottomRightText)
}
```

Es ist noch nicht ganz fertig. Wir müssen nur noch die Spalten und die zwei Diagonalen prüfen...

```kt
private fun isWinner(): Boolean {
    val horizontal =  areEqual(topLeftText, topCenterText, topRightText) ||
            areEqual(centerLeftText, centerCenterText, centerRightText) ||
            areEqual(bottomLeftText, bottomCenterText, bottomRightText)
    val vertical = areEqual(topLeftText, centerLeftText, bottomLeftText) ||
            areEqual(topCenterText, centerCenterText, bottomCenterText) ||
            areEqual(topRightText, centerRightText, bottomRightText)
    val diagonal = areEqual(topLeftText, centerCenterText, bottomRightText) ||
            areEqual(topRightText, centerCenterText, bottomLeftText)
    return horizontal || vertical || diagonal
}
```

## Ist das Spiel unentschieden?

Das ist einfach: das Spiel ist unentschieden, wenn alle Felder ausgefüllt wurden.

Um das herauszufinden, wäre praktisch, auf die Liste alle Textfelder zugreifen zu können: wir können `textFields` in der `onCreate()` Funktion in ein "Class field" umwandeln.

Android Studio kann ein Teil der Arbeit für dich erledigen: du kannst das `val` vor `textFields` löschen und dann auf die rote Glübirne klicken und "Create property 'textFields' property" auslösen.  
Das `textFields` Array wird damit _oben_ in der Klasse definiert (und nicht mehr in der `onCreate()` Funktion).

Es gibt noch ein kleines Problem: bevor `onCreate()` die Verbindung mit dem Layout herstellt, kann `textFields` nicht gefüllt werden. Wir müssen das ausdrücklich mit `lateinit` angeben (und implizit versprechen, dass wir `textFields` nicht brauchen, bevor es vollständig ist):

```kt
class MainActivity : AppCompatActivity() {

    private lateinit var textFields: Array<TextView>

    // ...
    
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        textFields = arrayOf(topLeftText, topCenterText, topRightText,
            centerLeftText, centerCenterText, centerRightText,
            bottomLeftText, bottomCenterText, bottomRightText)

    // ...
    }

    // ...
}
```

![](images/tic-tac-toe-lateinit-text-fields.gif)

Und jetzt können wir prüfen, ob das Spiel unentschieden endet. Falls alle Felder bereits ausgefüllt sind ist es Unentschieden:

```kt
if (isWinner()) {
    statusText.text = "${currentSign} hat gewonnen"
} else if (textFields.all { it.text != "" }) {
    statusText.text = "Unentschieden"
} else {
    currentSign = if (currentSign == "X") "0" else "X"
    statusText.text = "${currentSign} ist an der Reihe"
}
```

Die `else if` Bedingung sieht sehr einfach aus: aber werden wir sie ohne weitere Kommentare auch verstehen, wenn wir uns in der Zukunft wieder mit diesem Code beschäftigen?

Es ist doch besser eine kurze `isTie()` Funktion zu schreiben:

```kt
private fun isTie() {
	return textFields.all { it.text != "" }
}
```

Wir können auch das _Refactor_-Werkzeug von Android Studio gebrauchen:

![](images/tic-tac-toe-refactor-is-tie.gif)

Damit lernen wir, dass Kotlin eine spezielle Schreibart bietet, für Funktionen, die aus einer einzelne Zeile bestehen:

```kt
private fun isTie() = textFields.all { it.text != "" }
```

Die Logik des Codes sieht nun so aus:

```kt
if (isWinner()) {
    statusText.text = "${currentSign} hat gewonnen"
} else if (isTie()) {
    statusText.text = "Unentschieden"
} else {
    currentSign = if (currentSign == "X") "0" else "X"
    statusText.text = "${currentSign} ist an der Reihe"
}
```

## Jedes Spiel hat ein Ende

Auch nachdem jemand gewonnen hat, fügt jedes weitere Klick ein Zeichen hinzu, bis alle Felder ausgefüllt sind. Das wollen wir ändern und dann das Spiel neustarten.

Dafür brauchen wir:

- Eine `gameOver` Variable die wir auf `true` setzen wenn, das Spiel zu Ende geht.
- Eine `if` Bedingung die prüft, dass das Spiel zu Ende ist.
- Eine `resetGame` Funktion, die das Brett wieder leert.

Zuerst definieren wir die `gameOver` Klassenfeld:

```kt
class MainActivity : AppCompatActivity() {

    private lateinit var textFields: Array<TextView>
    private var currentSign = "X"
    private var gameOver = false

    override fun onCreate(savedInstanceState: Bundle?) {
        // ...
    }
    // ...
}
```

... und dann die `resetGame` Funktion...


```kt
class MainActivity : AppCompatActivity() {

    // ..

    override fun onCreate(savedInstanceState: Bundle?) {
        // ...
    }

    // ...

    private fun resetGame() {
        gameOver = false
        currentSign = "X"
        statusText.text = "${currentSign} ist an der Reihe"
        for (field in textFields) {
            field.text = ""
        }
    }
}
```

... und schliesslich `gameOver` als `true` setzen, wenn jemand gewonnen hat oder das Spiel unentschieden ist und dann, beim nächsten Klick, das Spiel neustarten:

```kt
for (textField in textFields) {
    textField.setOnClickListener { view ->
        view as TextView
        if (gameOver) {
            resetGame()
        } else {
            if (view.text == "") {
                view.text = currentSign
                if (isWinner()) {
                    statusText.text = "${currentSign} hat gewonnen"
                    gameOver = true
                } else if (isTie()) {
                    statusText.text = "Unentschieden"
                    gameOver = true
                } else {
                    currentSign = if (currentSign == "X") "0" else "X"
                    statusText.text = "${currentSign} ist an der Reihe"
                }
            }
        }
    }
}
```

## Was haben wir gelernt?

- Felder aus dem Layout _lesen_ und _schreiben_
- Mit Android Studio code zu schreiben.
- auf "Klick"/"Touch" Events zu reagieren
- Refactoring: nachdem wir Code geschrieben haben, können wir über die Bücher gehen, und schauen wie wir den Code verbessern können, ohne neue Features hinzufügen. Android Studio gibt uns mächtige Tools um das Refactoring zu beschleunigen.

## Todo

- Resize the table to fit the screen.
- Check that the screencast and screenshot match the final code.
- Create a repository with commits for each step.
