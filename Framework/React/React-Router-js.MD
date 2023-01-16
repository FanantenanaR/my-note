# Routage pour React JS

Version utilisé: React Router V6

## Installation

```CMD 
npm install react-router-dom@6
```

## Utilisation

### Import
```JS
import {
  BrowserRouter,
  Routes,
  Route,
} from "react-router-dom";
```

### Routage
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

### Navigation
Pour naviguer avec des liens cliquables, il faut utiliser `Link`, importé comme:

```JSX
import { Link } from "react-router-dom";
```

puis 

```JSX
<Link to="/" > Home </Link>
```

Mais pour plus de pouvoir, on peut aussi utiliser `useNavigate` 
```JSX
import { useNavigate } from "react-router-dom";

function AnyRandowComponents() {
  let navigate = useNavigate();
  return (
    <div>
      <NewInvoiceForm
        onSubmit={async (event) => {
          navigate(`/thelink/${anyvariable.id}`);
        }}
      />
    </div>
  );
}
```

### Décomposition d'URL

Pour obtenir les variables passés en URL comme `/teams/:id`, il faut utiliser `useParams`, importé comme

```JSX
import { useParams } from 'react-router-dom';
```

puis 

```JSX
const param = useParams()

const idTeam = param.id 
```

### "Not Found" Routes
On peut aussi prévoir les cas de `404 NOT FOUND` en assignant une route à ceci, `path=*`

### Multiple Routes
On peut aussi definir plusieur `Routes` comme

```JSX
function App() {
  return (
    <div>
      <Sidebar>
        <Routes>
          <Route path="/" element={<MainNav />} />
          <Route
            path="dashboard"
            element={<DashboardNav />}
          />
        </Routes>
      </Sidebar>

      <MainContent>
        <Routes>
          <Route path="/" element={<Home />}>
            <Route path="about" element={<About />} />
            <Route path="support" element={<Support />} />
          </Route>
          <Route path="dashboard" element={<Dashboard />}>
            <Route path="invoices" element={<Invoices />} />
            <Route path="team" element={<Team />} />
          </Route>
          <Route path="*" element={<NotFound />} />
        </Routes>
      </MainContent>
    </div>
  );
}
```
et ces routes se comporteront selon leur definition respectif.
