<p align="center">
  <img src="Assets/Sprites/Titlescreen.png" width="720" alt="UNIverse title screen: an Ontario Tech University building sketch with a green Play button" />
</p>

<h1 align="center">Game of Uni (UNIverse)</h1>

<p align="center">
  A four-player, pass-and-play board game about surviving university, built in Unity.
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Unity-2022.3.9f1-000000?style=for-the-badge&logo=unity&logoColor=white" alt="Unity 2022.3.9f1" />
  <img src="https://img.shields.io/badge/C%23-scripts-512BD4?style=for-the-badge&logo=csharp&logoColor=white" alt="C#" />
  <img src="https://img.shields.io/badge/Platform-Windows-0078D6?style=for-the-badge&logo=windows&logoColor=white" alt="Windows" />
  <img src="https://img.shields.io/badge/Players-4-f59e0b?style=for-the-badge" alt="4 players" />
</p>

---

## About

Four students start at **First Semester** and work their way through eight semesters, two sets of finals and one big life choice. Every turn you flip a coin: heads draws an **Opportunity** card (scholarships, internships, TA jobs), tails draws an **Expense** card (textbooks, a broken phone, residence fees). After fourth year you choose between a **Master's** degree or going straight into a **Job**, and whoever reaches the end with the most money wins.

<p align="center">
  <img src="Assets/Sprites/Board.png" width="520" alt="Hand-drawn game board: eight semesters with finals, Expense and Opportunity card piles, and a split path to Masters or Job before the End square" />
</p>

## How to play

| Key | Action |
| :--- | :--- |
| <kbd>Space</kbd> | Start the game, continue past the rules screen, take your turn |
| <kbd>Enter</kbd> | Accept the card you drew and pass the turn |
| <kbd>←</kbd> | At the crossroads: pursue a **Master's** (−$1,000, then two Opportunity cards) |
| <kbd>→</kbd> | At the crossroads: take a **Job** (+$500, then one more coin flip) |
| <kbd>Esc</kbd> | Restart the board |

1. Everyone starts with $10,000. Player 1 goes first: press <kbd>Space</kbd> to flip the coin.
2. Read your card and press <kbd>Enter</kbd>. Your balance updates and you move one tile.
3. Play passes to the next student. Anyone who reaches **End** sits out the remaining turns.
4. When all four players finish, the scoreboard shows everyone's final balance. Press <kbd>Space</kbd> to go back to the title screen.

The decks hold 14 Opportunity cards (up to **+$5,000**) and 15 Expense cards (up to **−$5,000**), defined in [`CardData.cs`](Assets/Scripts/CardData.cs).

## Download and run

A prebuilt Windows version is in [`Releases/1.1`](Releases/1.1). Clone the repo (or use **Code → Download ZIP**) and run `Releases/1.1/Game of Uni.exe`. No install needed.

## Open in Unity

1. Install **Unity 2022.3.9f1** (LTS) through Unity Hub.
2. Clone the repo and open the folder as a project:
   ```bash
   git clone https://github.com/ayushkarun0125-hub/Game-of-Uni---Game-Dev.git
   ```
3. Open `Assets/Scenes/TitleScreen.unity` and press **Play**.

Scene order: `TitleScreen` → `Tutorial` → `MainGame` → `Scoreboard`.

## How it's built

| Script | What it does |
| :--- | :--- |
| [`TurnManager.cs`](Assets/Scripts/TurnManager.cs) | Rotates turns between the four players, tracks balances and who has finished, loads the scoreboard when everyone is done |
| [`Player.cs`](Assets/Scripts/Player.cs) | Reads input for the active player, resolves the tile they're on (coin toss, decision or opportunity-only), and lerps the token and camera to the next tile |
| [`Tile.cs`](Assets/Scripts/Tile.cs) | Per-tile data set in the editor: path ID, position, tile type and any fixed money change |
| [`CardData.cs`](Assets/Scripts/CardData.cs) | Opportunity and Expense decks as text-to-amount dictionaries |
| [`GameUIManager.cs`](Assets/Scripts/GameUIManager.cs) | Shows and hides the card overlays and pauses the board while a card is open |
| [`Scoreboard.cs`](Assets/Scripts/Scoreboard.cs) | Renders the final balances |
| [`BetweenSceneInputManager.cs`](Assets/Scripts/BetweenSceneInputManager.cs) | Stops one key press from firing in two scenes or for two players |

The board is split into three paths: the main semester track, and the Master's and Job branches after the crossroads. Each tile is keyed by path and position (`a1`, `b1`, `c1`, …), so the player only stores where it is and the board drives the rest.

## Project layout

```
Assets/
├── Scenes/      TitleScreen, Tutorial, MainGame, Scoreboard
├── Scripts/     Game logic (C#)
├── Prefabs/     Player tokens 1–4, hex tile
└── Sprites/     Board, title and rules screens, card art
Releases/        Windows builds (1.0, 1.1)
```

---

<p align="center"><sub>Made in 2023 by The Squad.</sub></p>
