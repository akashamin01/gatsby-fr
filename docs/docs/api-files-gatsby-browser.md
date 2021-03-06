---
title: Le fichier API gatsby-browser.js
---

Le fichier `gatsby-browser.js` vous permet de répondre aux actions dans le navigateur et d'encapsuler votre site dans des composants supplémentaires. Les [APIs navigateur de Gatsby](/docs/browser-apis) vous offre de nombreuses options pour interagir avec le [côté client](/docs/glossary#client-side) de Gatsby.

Les APIs `wrapPageElement` et `wrapRootElement` existent à la fois dans le navigateur et dans [les APIs de Server-Side Rendering (SSR)](/docs/ssr-apis). Si vous en utilisez un, demandez-vous si vous devez l'implémenter dans `gatsby-ssr.js` et `gatsby-browser.js` afin que les pages générées via SSR avec Node.js soient les mêmes après avoir été [hydratées](/docs/glossary#hydration) avec le navigateur JavaScript.

Pour utiliser les APIs du navigateur, créez un fichier à la racine de votre site à `gatsby-browser.js`. Exportez chaque API que vous souhaitez utiliser à partir de ce fichier.

```jsx:title=gatsby-browser.js
const React = require("react")
const Layout = require("./src/components/layout")

// Affiche un message lorsque la route client change
exports.onRouteUpdate = ({ location, prevLocation }) => {
  console.log("nouveau chemin", location.pathname)
  console.log("ancien chemin", prevLocation ? prevLocation.pathname : null)
}

// Encapsule chaque page dans un composant
exports.wrapPageElement = ({ element, props }) => {
  return <Layout {...props}>{element}</Layout>
}
```
