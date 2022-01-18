# Hub-react-call-api
workshop d'utilisation de react pour faire des appels à des api

Pour commencer créer un projet react (installer node js avant)

<!--sec data-title="Your first command: OS X and Linux" data-id="OSX_Linux_whoami" data-collapse=true ces-->

    $ npx create-react-app mon-app
    $ cd mon-app
    $ npm start
    
<!--endsec-->

Cela va créer l'arboresrance suivante:

![alt text](https://github.com/Excelsiort/Hub-react-call-api/blob/main/tree.png)

Pour ce que nous allons faire vous pouvez supprimer tout les fichier du dossier public à part index.html et tout les fichiers de src à part app.js et index.js

Remplacer le contenu de index.js par ça: 

```javascript
import React from 'react';
import ReactDOM from 'react-dom';
import App from './App';

ReactDOM.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>,
  document.getElementById('root')
);



```


Et le contenu de app.js par ça:

```javascript
function App() {
  return (
     <p>hello world</p>
  );
}

export default App;


```

Pour lancer l'application:

<!--sec data-title="Your first command: OS X and Linux" data-id="OSX_Linux_whoami" data-collapse=true ces-->

    $ npm start
    
<!--endsec-->

Elle sera sur http://localhost:3000/

Maintenant nous allons installer Axios (un client HTTP basé sur les Promesses) pour faire nos requêtes:

<!--sec data-title="Your first command: OS X and Linux" data-id="OSX_Linux_whoami" data-collapse=true ces-->

    $ npm install axios
    
<!--endsec-->

Nous allons créer un dossier component à la racine et un fichier bitcoinRate.js à l'interieur debutant avec les imports suivants:

```javascript
import React,{useEffect,useState} from 'react'
import axios from 'axios'

```

Puis nous allons faire la délaration du component:

```javascript
const bitcoinRate = () => {
    return (
        <div>
            
        </div>
    );
};

export default bitcoinRate;

```

Tout ce qui se trouve au dessus du return sera en javascript et servira à rendre les rendus dynamiques, ce qui se trouve dans le return sera en jsx (très proche du html) pour faire le rendu graphique, le style sera appliqué avec du css classique (sass possible).

Nous allons maintenant voir comment afficher les données de cette api publique (https://api.coindesk.com/v1/bpi/currentprice.json) sur notre application.
