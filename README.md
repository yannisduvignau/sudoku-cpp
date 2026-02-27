# 🔢 sudoku-cpp

> A **console-based Sudoku game** written in **C++** — featuring grid display, user input, rule validation, and an automatic backtracking solver.

---

## 📋 Description

**sudoku-cpp** is a terminal Sudoku game implemented in C++. The project separates the Sudoku grid model (`sudoku`) from the game utilities (`game-tools`), providing a clean modular architecture. Players can fill in the grid manually or let the built-in **backtracking algorithm** solve it automatically.

Developed as a university project by **GUIHENEUF** and **DUVIGNAU**, the full technical report is included as a PDF.

---

## 🗂️ Project Structure

```
sudoku-cpp/
├── main.cpp                           # Entry point — launches the game, handles the main menu
├── sudoku.h / sudoku.cpp              # Sudoku model — 9×9 grid, validation rules, backtracking solver
├── game-tools.h / game-tools.cpp      # Game utilities — display, user input, hints, move handling
└── sudoku-GUIHENEUF-DUVIGNAU.pdf      # Project report — specifications, design, and test cases
```

---

## 🛠️ Tech Stack

| Layer | Technology |
|-------|-----------|
| Language | C++ / C (C++11) |
| Build | `g++` / `clang++` |
| Interface | Terminal (stdin / stdout) |
| Algorithm | Backtracking (recursive depth-first search) |
| Data structure | 9×9 integer matrix |

---

## 🧠 How It Works

### Grid Representation

The Sudoku board is stored as a **9×9 integer matrix**. Empty cells are represented by `0`. The grid is divided into 9 **3×3 sub-grids (boxes)**.

```
┌───────┬───────┬───────┐
│ 5 3 . │ . 7 . │ . . . │
│ 6 . . │ 1 9 5 │ . . . │
│ . 9 8 │ . . . │ . 6 . │
├───────┼───────┼───────┤
│ 8 . . │ . 6 . │ . . 3 │
│ 4 . . │ 8 . 3 │ . . 1 │
│ 7 . . │ . 2 . │ . . 6 │
├───────┼───────┼───────┤
│ . 6 . │ . . . │ 2 8 . │
│ . . . │ 4 1 9 │ . . 5 │
│ . . . │ . 8 . │ . 7 9 │
└───────┴───────┴───────┘
```

### Validation Rules

For any cell `(row, col)`, a value `n` is valid if:
- `n` does not already appear in the **same row**
- `n` does not already appear in the **same column**
- `n` does not already appear in the **same 3×3 box**

### Backtracking Solver

```
findEmptyCell()
      │
      ▼
  tryValues 1–9
      │
      ├── isValid(row, col, n)?
      │         │
      │         ├── YES → place n → recurse deeper
      │         │               │
      │         │               ├── solved → return true ✅
      │         │               └── failed → remove n (backtrack) ↩
      │         │
      │         └── NO  → try next value
      │
      └── no value works → return false (trigger backtrack) ↩
```

---

## 🚀 Getting Started

### Prerequisites

- A C++ compiler: `g++` (GCC) or `clang++`
- Linux, macOS, or Windows (with MinGW or WSL)

---

### 1. Clone the repository

```bash
git clone https://github.com/yannisduvignau/sudoku-cpp.git
cd sudoku-cpp
```

### 2. Compile

```bash
g++ -std=c++11 -o sudoku main.cpp sudoku.cpp game-tools.cpp
```

With warnings enabled (recommended):

```bash
g++ -std=c++11 -Wall -Wextra -o sudoku main.cpp sudoku.cpp game-tools.cpp
```

### 3. Run

```bash
./sudoku
```

---

## 🎮 Gameplay

```
=============================
       SUDOKU — MENU
=============================
  [1] Play (manual input)
  [2] Solve automatically
  [3] Quit
=============================
> _
```

| Action | Description |
|--------|-------------|
| Enter a value | Type `row col value` (e.g. `3 5 7`) to place 7 at row 3, col 5 |
| Validate move | The game checks row, column, and 3×3 box constraints instantly |
| Auto-solve | The backtracking solver fills the entire grid in one step |
| Display grid | The board is reprinted after every move with box separators |
| Win detection | The game congratulates the player when the grid is fully and correctly filled |

---

## 🧩 Module Overview

### `sudoku.h / sudoku.cpp` — Sudoku Model

| Function | Description |
|----------|-------------|
| `initGrid()` | Initializes the 9×9 grid with a starting puzzle |
| `isValid(row, col, n)` | Returns `true` if placing `n` at `(row, col)` respects all rules |
| `solve()` | Recursive backtracking solver — returns `true` when the grid is solved |
| `findEmptyCell(row, col)` | Finds the next cell containing `0` |
| `isSolved()` | Returns `true` if all 81 cells are filled and valid |
| `getCell(row, col)` | Returns the current value at a given cell |
| `setCell(row, col, n)` | Places a value in the grid after validation |

### `game-tools.h / game-tools.cpp` — Game Utilities

| Function | Description |
|----------|-------------|
| `displayGrid()` | Prints the 9×9 grid with 3×3 box separators to the terminal |
| `getUserInput()` | Reads and parses the `row col value` command from stdin |
| `displayMenu()` | Shows the main menu |
| `displayWin()` | Prints the victory message |
| `displayError()` | Prints an invalid move error message |

---

## 🧠 Concepts Covered

| Topic | Description |
|-------|-------------|
| Backtracking | Recursive DFS to solve constraint satisfaction problems |
| 2D arrays | 9×9 integer grid manipulation in C++ |
| Constraint checking | Row, column, and 3×3 box uniqueness validation |
| Modular design | Separation of model (`sudoku`) from utilities (`game-tools`) |
| Terminal I/O | Reading user input and formatting structured grid output |
| Header / source separation | `.h` declarations with `.cpp` implementations |

---

## 📄 Project Report

The report `sudoku-GUIHENEUF-DUVIGNAU.pdf` contains:

- Project specifications and objectives
- Algorithm design — backtracking explanation with diagrams
- Class and function descriptions
- Test cases and validation examples
- Conclusions and potential improvements

---

## 🤝 Contributing

1. Fork the project
2. Create your branch (`git checkout -b feature/difficulty-levels`)
3. Commit your changes (`git commit -m 'Add easy/medium/hard difficulty presets'`)
4. Push to the branch (`git push origin feature/difficulty-levels`)
5. Open a Pull Request

---

## 👥 Authors

**Yannis Duvignau** — [GitHub](https://github.com/yannisduvignau)  
**GUIHENEUF**

---

## 📚 Resources

- 📖 [Backtracking — Sudoku Solver (GeeksForGeeks)](https://www.geeksforgeeks.org/sudoku-backtracking-7/)
- 🔢 [Sudoku solving algorithms — Wikipedia](https://en.wikipedia.org/wiki/Sudoku_solving_algorithms)
- 🧑‍💻 [C++ Standard Library Reference](https://en.cppreference.com/)
- 🎯 [Constraint Satisfaction Problems](https://en.wikipedia.org/wiki/Constraint_satisfaction_problem)

---

## 📄 License

This project is distributed under an open license. See the `LICENSE` file for more details.
