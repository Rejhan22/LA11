---
icon: computer-mouse
---

# Event Handling

Mit React können wir unserem JSX **Event-Handler** hinzufügen. Event-Handler sind unsere eigenen Funktionen, die als Antwort auf Interaktionen wie Klicken, Hovering, Fokussieren von Formulareingaben usw. ausgelöst werden.

## Event-Handler hinzufügen

Um einen Event-Handler hinzuzufügen, definieren wir zunächst eine Funktion und übergeben diese dann als Prop an das entsprechende JSX-Tag.

<pre class="language-tsx"><code class="lang-tsx">const Button = () => {
  const handleClick = () => alert('You clicked me!');

  return (
    &#x3C;button <a data-footnote-ref href="#user-content-fn-1">onClick={handleClick}</a>>
      Click me
    &#x3C;/button>
  );
}

export default Button;
</code></pre>

Es ist natürlich auch möglich einen Event-Handler inline zu definieren.

```tsx
<button onClick={() => alert('You clicked me!')}>
```

{% hint style="info" %}
Es gibt noch viele weitere Events:&#x20;

* `onMouseEnter`
* `onChange`
* `onCopy`
* ...
  {% endhint %}

## Event-Handlers als Props

Oft möchte man, dass die übergeordnete Komponente den Event-Handler einer untergeordneten Komponente festlegt. Zum Beispiel Buttons: Je nachdem, wo man eine `Button`-Komponente verwendet, möchte man vielleicht eine andere Funktion ausführen - vielleicht spielt eine einen Film ab und eine andere lädt ein Bild hoch.\


Wir übergeben dazu ein Prop, die die Komponente von der übergeordneten Komponente erhält, als Event-Handler, etwa so:

{% tabs %}
{% tab title="Button" %}
{% code title="Button.jsx" %}
```tsx
const Button = ({ onClick, children }) => {
  return (
    <button onClick={onClick}>
      {children}
    </button>
  );
}

export default Button;
```
{% endcode %}
{% endtab %}

{% tab title="Upload Button" %}
{% code title="UploadButton.jsx" %}
```tsx
const UploadButton = () => {
  return (
    <Button onClick={() => alert('Uploading')}>
      Play "{movieName}"
    </Button>
  );
}

export default UploadButton;
```
{% endcode %}
{% endtab %}

{% tab title="Play Button" %}
{% code title="PlayButton.jsx" %}
```tsx
const PlayButton = ({ movieName }) => {
  const handlePlayClick = () => alert(`Playing ${moviename}!`);

  return (
    <Button onClick={handlePlayClick}>
      Play "{movieName}"
    </Button>
  );
}

export default PlayButton;
```
{% endcode %}
{% endtab %}

{% tab title="Toolbar" %}
{% code title="Toolbar.jsx" %}
```tsx
const Toolbar = () => {
  return (
    <div>
      <PlayButton movieName="Kiki's Delivery Service" />
      <UploadButton />
    </div>
  );
}

export default Toolbar;
```
{% endcode %}
{% endtab %}
{% endtabs %}

Hier stellt die `Toolbar`-Komponente einen `PlayButton` und einen `UploadButton` dar:

* `PlayButton` übergibt `handlePlayClick` als `onClick`-Prop an den `Button` darin.
* `UploadButton` übergibt `() => alert('Uploading!')` als `onClick`-Prop an den `Button` im Inneren.

Schliesslich akzeptiert die`Button`-Komponente eine Eigenschaft namens `onClick`. Sie übergibt dieses Prop direkt an den eingebauten Browser `<button>` mit `onClick={onClick}`. Dadurch wird React angewiesen, die übergebene Funktion bei einem Klick aufzurufen.

Wenn man ein [Designsystem](https://uxdesign.cc/everything-you-need-to-know-about-design-systems-54b109851969) verwendet, ist es üblich, dass Komponenten wie Schaltflächen zwar Styling enthalten, aber kein Verhalten festlegen. Stattdessen werden Komponenten wie `PlayButton` und `UploadButton` Event-Handler weitergeben.

[^1]: Hier wird die Methode `handleClick` ausgeführt, wenn ein Klick stattfindet

---
icon: plus
---

# State-Variable hinzufügen

Um eine State-Variable hinzuzufügen, müssen wir `useState` von React importieren und dann den `useState`-Hook nutzen.

```tsx
const [step, setStep] = useState(1);
```

`step` ist eine State-Variable, während `setState` die Setter-Funktion ist.

{% hint style="info" %}
Die `[` und `]` Syntax wird hier als [Array-Destructuring](https://javascript.info/destructuring-assignment) bezeichnet und ermöglicht das Lesen von Werten aus einem Array. Das von `useState` zurückgegebene Array hat immer genau zwei Elemente.
{% endhint %}

```tsx
const App = () => {
  const [step, setStep] = useState(1);

  const handleNext = () => {
    if (step < 3) setStep((step) => step + 1);
  };

  const handlePrevious = () => {
    if (step > 1) setStep((step) => step + 1);
  };

  return (
    <div className="steps">
      <div className="numbers">
        <div className={`${step >= 1 ? 'active' : ''}`}>1</div>
        <div className={`${step >= 2 ? 'active' : ''}`}>2</div>
        <div className={`${step >= 3 ? 'active' : ''}`}>3</div>
      </div>

      <p className="message">
        Step {step}: {messages[step - 1]}
      </p>

      <div className="buttons">
        <button
          onClick={handlePrevious}
          style={{ backgroundColor: '#7950f2', color: '#ffffff' }}
        >
          Previous
        </button>
        <button
          onClick={handleNext}
          style={{ backgroundColor: '#7950f2', color: '#ffffff' }}
        >
          Next
        </button>
      </div>
    </div>
  );
};

export default App;
```

## Dein erster Hook

In React, `useState`, und andere Funktionen, die mit "`use`" starten, werden **Hook** genannt.&#x20;

_Hooks_ sind spezielle Funktionen, die nur verfügbar sind, während React am [Rendern ](https://react.dev/learn/render-and-commit#step-1-trigger-a-render)ist. Sie lassen uns in verschiedene React Features "einhaken".

State ist nur eine dieser Features, wir werden noch viele weiter Hooks kennenlernen.

{% hint style="warning" %}
**Hooks - Funktionen, die mit `use` starten - können nur auf oberster Ebene der Komponente aufgerufen werden.** Hooks können nicht in Konditionen, Loops oder verschachtelten Funktionen aufgerufen werden.
{% endhint %}

## Aufbau von `useState`

Wenn du [`useState`](https://react.dev/reference/react/useState) aufrufst, sagst du React, dass diese Komponente sich etwas merken soll:

```tsx
const [index, setIndex] = useState(0);
```

In diesem Fall möchtest du, dass React sich `index` merkt.

{% hint style="info" %}
Die Konvention für die Namen, der State-Variable und des Setters sind `const [something, setSomething]`
{% endhint %}

Das einzige Argument, welches du `useState` mitgeben musst, ist der **Initialwert** deiner State-Variable. In diesem Beispiel ist `index`'s Initialwert `0`.

***

Jedes Mal, wenn unsere Komponente gerendert wird, gibt uns`useState` einen Arrays mit zwei Werten:

1. Die **State-Variable** (`index`) mit dem Wert, der gespeichert ist.
2. Die **State-Setter-Funktion**  (setIndex) wleche die State-Variable aktualisieren kann und React triggert, die Komponente erneut zu rendern.

Hier siehst du, wie das in Aktion passiert:

```tsx
const [index, setIndex] = useState(0);
```

1. **Deine Komponente wird zum ersten Mal gerendert.** Weil du `0` an `useState` übergeben hast, gibt es uns `[0, setIndex]` zurück. React merkt sich `0` als letzten Wert.
2. **Du aktualisierst den State.** Wenn ein User auf einen Button klickt ruft er `setIndex(index + 1)` auf. `index` ist `0`, also ist es `setIndex(1)`. Das sagt React, dass `index` jetzt `1` ist und triggert einen re-render.
3. **Das zweite Rendern deiner Komponente.** React sieht immer noch `useState(0)`, aber da React sich _erinnert_, dass du `index` zu `1` gesetzt hast, gibt es uns `[1, setIndex]` zurück.
4. Und so weiter

---
icon: pen-field
---

# Formulare

In React gibt es mehrere Möglichkeiten Formulare zu erstellen, Controlled, Uncontrolled, `useForm`-Hook, etc.

## Controlled Forms

Mit **Controlled Forms** speichern wir jedes Input-Field in einer State-Variable und setzen der Wert jedes Inputs nach jedem Re-Render der Komponente. Das gibt uns mehr Möglichkeiten, um Validierungen oder Manipulationen vorzunehmen (bspw. um Telefonnummern korrekt zu formatieren).

<pre class="language-jsx"><code class="lang-jsx">const Form = ({ onAddItem }) => {
  <a data-footnote-ref href="#user-content-fn-1">const [description, setDescription] = useState('');</a>
  <a data-footnote-ref href="#user-content-fn-2">const [quantity, setQuantity] = useState(1);</a>

  const handleSubmit = (e) => {
    e.preventDefault();

    <a data-footnote-ref href="#user-content-fn-3">if (!description.trim()) return;</a>

    onAddItem({ description, quantity, packed: false, id: Date.now() });

    <a data-footnote-ref href="#user-content-fn-4">setDescription('');</a>
    <a data-footnote-ref href="#user-content-fn-5">setQuantity(1);</a>
  };

  return (
    &#x3C;form className="add-form" onSubmit={<a data-footnote-ref href="#user-content-fn-6">handleSubmit</a>}>
      &#x3C;h3>What do you need for your 😍 trip?&#x3C;/h3>

      &#x3C;select
        value={<a data-footnote-ref href="#user-content-fn-7">quantity</a>}
        <a data-footnote-ref href="#user-content-fn-8">onChange={(e) => setQuantity(Number(e.target.value))}</a>
      >
        {Array.from({ length: 20 }, (_, i) => i + 1).map((num) => (
          &#x3C;option value={num} key={num}>
            {num}
          &#x3C;/option>
        ))}
      &#x3C;/select>

      &#x3C;input
        type="text"
        placeholder="Item..."
        value={<a data-footnote-ref href="#user-content-fn-9">description</a>}
        <a data-footnote-ref href="#user-content-fn-10">onChange={(e) => setDescription(e.target.value)}</a>
      />

      &#x3C;button type="submit">Add&#x3C;/button>
    &#x3C;/form>
  );
};

export default Form;
</code></pre>

### Objekte

Anstatt für jedes Input-Field eine eigene State-Variable zu erstellen, können wir ein einzelnes Objekt nutzen.

<pre class="language-tsx"><code class="lang-tsx">const Form = ({ onAddItem }) => {
  <a data-footnote-ref href="#user-content-fn-11">const [item, setItem] = useState</a>({
    description: '',
    quantity: 1,
    packed: false,
    id: Date.now(),
  });

  const handleSubmit = (e) => {
    e.preventDefault();

    if (!item.description.trim()) return;

    onAddItem(item);

    setItem({ description: '', quantity: 1, packed: false, id: Date.now() });
  };

  <a data-footnote-ref href="#user-content-fn-12">const handleChange = (e)</a> => {
    const { name, value } = e.target;
    setItem((prevItem) => ({ ...prevItem, [name]: value }));
  };

  return (
    &#x3C;form className="add-form" onSubmit={handleSubmit}>
      &#x3C;h3>What do you need for your 😍 trip?&#x3C;/h3>

      &#x3C;select
        <a data-footnote-ref href="#user-content-fn-13">name="quantity</a>"
        value={item.quantity}
        <a data-footnote-ref href="#user-content-fn-14">onChange={(e) => handleChange(e)}</a>
      >
        {Array.from({ length: 20 }, (_, i) => i + 1).map((num) => (
          &#x3C;option value={num} key={num}>
            {num}
          &#x3C;/option>
        ))}
      &#x3C;/select>

      &#x3C;input
        type="text"
        placeholder="Item..."
        <a data-footnote-ref href="#user-content-fn-15">name="description"</a>
        value={item.description}
        <a data-footnote-ref href="#user-content-fn-16">onChange={(e) => handleChange(e)}</a>
      />

      &#x3C;button type="submit">Add&#x3C;/button>
    &#x3C;/form>
  );
};

export default Form;
</code></pre>

### Validierung

{% hint style="danger" %}
TODO
{% endhint %}

## Uncontrolled Forms

{% hint style="danger" %}
TODO
{% endhint %}

## useForm-Hook

{% hint style="danger" %}
TODO
{% endhint %}

[^1]: State-Variable für das erste Input-Field

[^2]: State-Variable für das zweite Input-Field

[^3]: Validierungen (Können auch in eine externe Funktion extrahiert werden)

[^4]: State zurücksetzen, nachdem Formular übermittelt wurde

[^5]: State zurücksetzen, nachdem Formular übermittelt wurde

[^6]: Funktion, die beim Absenden des Formulars aufgerufen werden soll

[^7]: Der Wert kommt von der State-Variable

[^8]: State bei jeder Änderung aktualisieren

[^9]: Der Wert kommt von der State-Variable

[^10]: State bei jeder Änderung aktualisieren

[^11]: Objekt als State-Variable

[^12]: Generische `handleChange`-Funktion

[^13]: `name`-Attibut zwingend, um Field zu identifizieren (<mark style="background-color:red;">muss gleich heissen, wie Property im Objekt</mark>)

[^14]: `onChange`-Funktion aufrufen

[^15]: `name`-Attibut zwingend, um Field zu identifizieren (<mark style="background-color:red;">muss gleich heissen, wie Property im Objekt</mark>)

[^16]: `onChange`-Funktion aufrufen

