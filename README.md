# Vue.js (Project1)

## Tic-Tac-Toe Game

This Projects inspired from [tic-tac-toe-game](https://github.com/shammadahmed/tic-tac-toe-game), I just solved some __Bugs__.

### Game elements

* 2 Players (X and O)
* The Board Grid (3 rows × 3 columns = 9 cells)
* Scoreboard (The number of wins for each player)
* Number of match being played
* Player turn
* Restarting the game

## Workflow

* [×] Init the project with (vue-cli)
* [×] Add google fonts to (index.html): [Dosis & Permanent Marker]
* [×] Edit App component (change styles)
* [×] Create the grid component & styling it
* [×] Create the cell component & styling it
* [×] Specify Data Properties (APP)
  - Number of matches
  - Number of wins for each player
* [×] Specify Data Properties (GRID)
  - Active Player (X or O)
  - Game Status (turn - win - draw)
  - Status Message ( O's turn / X's turn )
  - Status Color
    - statusTurn (default) is yellow for a turn
    - statusWin is green for a win
    - statusDraw is gray for a draw
  - Number of moves played by both players  (max=9)
  - Winning Conditions
  - Mark placement for each cell
* [×] Specify Data Properties (CELL)
* [×] Event Bus
* [×] Start game (Listening For shots)
  - listen to 'shot' event
  - fill the respective cell number with the mark in the cells object
  - increment the number of moves
  - change the game status and change the active player
  - Check game status
* [×] Displaying the Status
* [×] Checking for a Win
* [×] Scoreboard
* [×] Restarting the Game
* [×] Number of Matches

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Lints and fixes files
```
npm run lint
```
