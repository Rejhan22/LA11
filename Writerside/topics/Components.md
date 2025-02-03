---
icon: chart-tree-map
---

# Komponenten

Komponenten sind das fundamentalste Konzept in React, da React-Applikationen vollständig aus Komponenten bestehen.

* Komponenten sind die **Bauklötze** unseres User Interfaces in React
* Teil der UI, der seine eigenen **Daten, Logik und Aussehen** hat
* Wir bauen komplexe UIs, indem wir **mehrere Komponenten bauen und diese kombinieren**
* Komponenten können **wiederbenutzt** werden, ineinander **verschachtelt** sein und Daten zwischen ihnen **übergeben**

## Komponente definieren

Eine Komponente ist im Grunde genommen eine einfache Funktion, die uns Markup zurückgibt:

```tsx
const Pizza = () => {
  return <div>Pizza</div>;
}

export default Pizza;
```

## Komponente nutzen

Die Komponente können wir nun in unserer `<App />`-Komponente nutzen:

```tsx
const App = () => {
  return <Pizza />;
}

export default App;
```

***

Nun wird der Text _Pizza_ auf unserer Webseite angezeigt. Natürlich können wir nicht nur Text in unserer Komponenten anzeigen, sondern auch alle anderen HTML-Tags, wie **Bilder**, **Videos**, **Code**, etc.

```tsx
const Pizza = () => {
  return (
    <div>
      <img src="/pizzas/spinaci.jpg" alt="Pizza Spinaci" />
      <h2>Pizza Spinaci</h2>
      <p>Tomato, mozarella, spinach, and ricotta cheese</p>
    </div>
  );
}

export default Pizza;
```

## Code

In unseren Komponenten können wir natürlich auch ganz normalen JavaScript-Code schreiben und die Variablen dann in unserem Markup nutzen.

```tsx
const Footer = () => {
  const hour = new Date().getHours();
  const openHour = 8;
  const closeHour = 22;
  const isOpen = hour >= openHour && hour <= closeHour;
  console.log(isOpen)

  return <footer>We're open from {openHour}:00 to {closeHour}:00</footer>;
}

export default Footer;
```

Vor unserem `return`-Statement können wir also jeglichen normalen JavaScript-Code ausführen. Um JavaScript-Code in unserem JSX anzeigen zu lassen nutzen wir `{}`.

## Komponentenbäume

Komponenten visualisieren uns, wie die Applikation aufgebaut ist.

<img src="../../../.gitbook/assets/file.excalidraw (2).svg" alt="Komponentenbaum einer Blog-Seite" class="gitbook-drawing">

So können wir einsehen, wie die Komponenten verschachtelt sind, wie die Beziehungen zueinander sind, etc.