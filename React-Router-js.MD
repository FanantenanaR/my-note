# Package de routage de composant pour React JS

## Version utilisé: React Router V6

### Installation

npm install react-router-dom@6

### Utilisation

#### Configuration:

##### Import
import {
  BrowserRouter,
  Routes,
  Route,
} from "react-router-dom";

###### Routage

<BrowserRouter>
  <Routes>
    <Route path="/" element={<App />}>
      <Route index element={<Home />} />
      <Route path="teams" element={<Teams />}>
        <Route path=":teamId" element={<Team />} />
        <Route path="new" element={<NewTeamForm />} />
        <Route index element={<LeagueStandings />} />
      </Route>
    </Route>
  </Routes>
</BrowserRouter>
