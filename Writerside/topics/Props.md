---
icon: sliders
---

# Props

Props werden genutzt, um Daten von einer **Parent-Komponente zu einer Child-Komponente** zu übergeben. Es ist ein essenzielles Tool, um Komponenten zu **konfigurieren** und **anzupassen**. Mit Props **kontrollieren** Parent-Komponenten wie Child-Komponenten aussehen und funktionieren.

**Alles Mögliche** kann als Props übergeben werden: Strings, Arrays, Objekte, Funktionen, sogar andere Komponenten.

## Props übergeben

Die Daten übergeben wir einfach über ein Attribut unserer Komponente:

```jsx
<Pizza
  name="Pizza Spinaci"
  ingredients="Tomato, mozarella, spinach, and ricotta cheese"
  photoName="pizzas/spinaci.jpg"
  price={12}
/>
```

## Props annehmen

In unserer Child-Komponente können wir ein Parameter namens `props` annehmen.

```jsx
const Pizza = (props) => {
  return (
    <div>
      <img src={props.photoName} alt={props.name} />
      <h3>{props.name}</h3>
      <p>{props.ingredients}</p>
    </div>
  );
}

export default Pizza;
```

{% hint style="info" %}
Wenn wir mit TypeScript arbeiten müssen wir noch den Typ für die Props definieren.
{% endhint %}

## Prop-Types

Mit Prop-Types können wir Props validieren und Fehler abfangen. Prop-Types ist eine Library die wir zuerst installieren müssen:

```bash
npm install -D prop-types
```

Danach können wir unsere Props wie folgt definieren:

<pre class="language-jsx"><code class="lang-jsx">Pizza.propTypes = {
  <a data-footnote-ref href="#user-content-fn-1">pizza</a>: PropTypes.shape({
    name: PropTypes.<a data-footnote-ref href="#user-content-fn-2">string</a>.<a data-footnote-ref href="#user-content-fn-3">isRequired</a>,
    ingredients: PropTypes.string.isRequired,
    price: PropTypes.number.isRequired,
    photoName: PropTypes.string.isRequired,
    soldOut: PropTypes.bool.isRequired,
  }).isRequired,
};
</code></pre>

Für mehr Informationen konsultiere die [offizielle Dokumentation](https://www.npmjs.com/package/prop-types?activeTab=readme).

[^1]: Wir definieren ein Prop `pizza` welches ein Objekt ist mit den Properties `name`, `soldOut`, etc.

[^2]: Datentyp des Properties

[^3]: Muss zwingend vorhanden sein