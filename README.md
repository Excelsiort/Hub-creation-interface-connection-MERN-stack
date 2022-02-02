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

Pour commencer nous allons utiliser la fonction useEffect (précédement import). Il s'agit d'un hook effect, cela permet d'executer du code pendant le cycle de vie d'un composant et notamement dans notre cas de récuperer les données et de les mettre à jour régulièrement.

```javascript
    useEffect(()=>{
    
    },[])

```

Le 1er paramètre est une fonction de rappel (un callback) qui sera exécute pour l'effet que vous souhaitez "écouter".<br/>
Le 2ème est optionnel et permet de définir l'état (state ou props) que l'on souhaite observer.

Nous allons désormais définir une fonction getBtcRate, il s'agira d'une fonction asynchrone qui va utiliser une promesse comme valeur de retour.

```javascript
    const getBtcRate = async () => {

    };

```

À l'interieur nous allons recupérer les données de l'api grace à la methoge get de axios via un try catch (cela permet "d'essayer du code" et de "catch" une erreur si cela ne fonctionne pas) et les stocker dans une variable temporaire:


```javascript
        try {
        const rateTmp = await axios.get('https://api.coindesk.com/v1/bpi/currentprice.json')
  
        } catch (err) {
            console.error(err.message);
        }
```

Nous allons maintenant stocker ces données dans une variable grace à useState (nous allons la déclarer en tout premier dans notre component):

```javascript
    const [btcRate, setRate]=useState([])
```
Ici btcRate correspond à notre variable, setRate à la methode pour en changer la valeur, useState à définir sa valeur lors de la déclaration.

Revenons à la fonction getBtcRate et recupérons les donnée dans notre nouvelle variable: 

```javascript
    setRate(rateTmp.data);
```

Il faut maintenant appeler getBtcRate dans notre useEffect:


```javascript
    useEffect(()=>{
        getBtcRate()
    },[])

```

Passons à l'affichage des données que nous avons récuperer, cela se passera à l'interieur de la div du return:

```jsx
       <div>
            <br/>
            {btcRate.chartName} rate: 
            <br/>
            <br/>
            Valeur: {btcRate.bpi?btcRate.bpi.EUR.rate:"chargement"}€
            <br/>
            Mis à jour le: {btcRate.time?btcRate.time.updated:"chargement"}
            <br/>
            <br/>
        </div>

```

Pour finir nous allons définir une méthode pour mettre à jour les données automatiquement sans avoir à recharger la page dans la fonction useEffect: 

```javascript
       const interval=setInterval(()=>{
          getBtcRate()
         },10000)
           
           
       return()=>clearInterval(interval)
```
Vous pouvez maintenant aller sur <a link="">excercices.md</a>
