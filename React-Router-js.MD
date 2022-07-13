# Package de routage de composant pour React JS

Version utilisé: React Router V6

## Installation

```CMD 
npm install react-router-dom@6
```

## Utilisation

### Configuration:

#### Import
```JS
  import {
    BrowserRouter,
    Routes,
    Route,
  } from "react-router-dom";
```

#### Routage
```JSX
    <BrowserRouter> 
        <Routes>
            <Route path="/" element={<App />}>
                <Route index element={<Home />} />
                <Route path="teams" element={<Teams />} >
                    <Route path=":teamId" element={<Team />} />
                    <Route path="new" element={<NewTeamForm />} />
                    <Route index element={<LeagueStandings />} />
                </Route>
            </Route>
        </Routes>
    </BrowserRouter>
```
Les composants filles ***héritent*** les liens de ces parents. 
Ici, par exemple, on aura:

- `/` comme route de base vers `App`
  -  `/index` qui appelera `Home`
  -  `/teams` => `Teams`
    -  `/teams/:teamId` => `Team`
    -  `/teams/new` => `NewTeamForm`
    -  `/teams/index` => `LeagueStandings`

#### Navigation
Pour naviguer avec des liens cliquables, il faut utiliser `Link`, importé comme:

```JSX
import { Link } from "react-router-dom";
```

puis 

```JSX
    <Link to="/" > Home </Link>
    <Link to="/teams" > Teams </Link>
```

