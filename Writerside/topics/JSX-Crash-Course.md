# JSX Crash Course

## Variablen

````JSX
const App = () => {
  const name = 'John';

  return (
    <>
      <div className="text-5xl">App</div>
      <p>Hello {name}</p>
    </>
  );
};
export default App;
````

### berechnungen mit Variablen 
````JSX
const App = () => {
  const name = 'John';
  const x = 10;
  const y = 20;

  return (
    <>
      <div className="text-5xl">App</div>
      <p>Hello {name}</p>
      <p>The sum of {x} and {y} is { x + y}</p>
    </>
  );
};
export default App;
````

### Listen mit Arrays
````JSX
const App = () => {
  const name = 'John';
  const x = 10;
  const y = 20;

  return (
    <>
      <div className="text-5xl">App</div>
      <p>Hello {name}</p>
      <p>The sum of {x} and {y} is { x + y}</p>
    </>
  );
};
export default App;
````

Die ``map()``-Methode wird verwendet, um durch ein Array zu iterieren und für jedes Element eine neue JSX-Komponente zu erstellen:
````JSX
names.map((name) => (
  <li>{name}</li>
))
````

Hier passiert Folgendes:

1. ``names`` ist ein Array mit den Strings ['Brad', 'Mary', 'Joe', 'Sara']
2. ``map()`` durchläuft jeden Namen im Array
3. Für jeden Namen wird ein ``<li>``-Element erstellt, das den Namen enthält
4. Das Ergebnis ist eine Liste von ``<li>``-Elementen

Wichtig zu beachten: In React sollte jedes Element in einer Liste eine eindeutige ``key`` Prop haben. In deinem Code wurde dies mit einem ESLint-Kommentar deaktiviert, aber die korrekte Implementierung wäre:
````JSX
names.map((name, index) => (
  <li key={index}>{name}</li>
))
````

## If-statement
1. Verzweigung der Rendering-Logik (wird ausserhalb des Returns geschrieben)
2. Prüft Bedingung, bevor etwas gerendert wird
3. Basierend auf Bedingung wird komplett andere Komponente zurückgegeben

````JSX
const loggedIn = true;

// Vollständige Verzweigung der Render-Logik
if(loggedIn) {
  return <h1>Hello Member</h1>
}
// Implizit: else return null
````

Eine andere vorgehensweise um ein If-statement zu machen, ist direkt im return

````JSX
const App = () => {
  const name = 'John';
  const x = 10;
  const y = 20;
  const names = ['Brad', 'Mary', 'Joe', 'Sara']
  const loggedIn = true;

  return (
    <>
      <div className="text-5xl">App</div>
      <p>Hello {name}</p>
      <p>
        The sum of {x} and {y} is { x + y}
      </p>
      <ul>
        { names.map((name, index) => (
          // eslint-disable-next-line react/jsx-key
          <li key ={index}> {name} </li>
        ))}
      </ul>
      { loggedIn ? <h1>Hello Member</h1> : <h1>Hello Guest</h1>}
    </>
  );
};
export default App;
````

Mit logischem AND-Operator (&&):
````JSX
return (
  <div>
    {loggedIn && <h1>Hello Member</h1>}
  </div>
)
````

Die Wahl der Methode hängt davon ab, was du erreichen möchtest:

- Nutze if/else außerhalb von return für komplett unterschiedliche Render-Logik
- Nutze den ternären Operator für einfache entweder/oder Entscheidungen innerhalb des JSX
- Nutze && für einfaches ein/ausblenden von Elementen

## Inline-Styles
````JSX
<p style={{ color: 'red', fontSize: '24px'}}>Hello {name}</p>
````

Wichtig! Kein CSS sonder JavaScript. Daher: font-size wird zu fontSize.

### in einer Variabel
Deklaration:
````JSX
const styles = {
    color: 'red',
    fontSize: '55px'
  }
````

Verwendung:
````JSX
<p style={styles}>Hello {name}</p>
````