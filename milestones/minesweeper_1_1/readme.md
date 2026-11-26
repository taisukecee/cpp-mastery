# Objective
This milestone's goal is applying lessons from C++: A Beginner's Guide. Anything outside of the book is out of this milestone's scope.

# Architecture
The following is the UML diagram for this milestone:

![UML Class Diagram of Minesweeper](https://img.plantuml.biz/plantuml/png/bLHTQy8m57tlhmXzgflr1uY8qw4Evf1ji8VXGsokDLi-IfCwHTnlNz9AROnkB9GGSixDlJddfWEbSQuBpe8WmyadJW65IfCGxGDanb3YdA3E3He1CnIxbJ2i50ev5Q2-03B8EqcMXGWhDCDKe5uFHUFs8qtNUiWAQA5-_tYO7OLGD1L041NQyBTlbEZrLNGAzfYhy5F1PxQCch2Kag47DMOuVT5OGmt4SLolRyjmRcgDMetDUxfQqQHWUeVckUIPFcqul8san91Lnl2kb2UgH5hQsIFESQvW93d7WgZZEOTAIANp8j7DlFj6j7FNBZfJmiDT7JtOKUfGpWqpgmkSiiT_PFTmDxi7UpvTObZJcWpRSU-BzuL14xDKLxoiB6Y8IEfbquplYkVvyohJb87DRVD5JbdRjblcpej-XWrWzi_86b5hcUiIdu2UO0vbpperrY8OXbsVMkZCGWiw_LC-XUxnCQH0Ba5L-PUmALRMiT-hBcsx8nyu0Q6RxHMORm22cD_A3m00)

<details>
    <summary>Code for the diagram</summary>
    
    @startuml

    package "std" {
        Board .* Cell

        class "minesweeper.cpp" as Main << (F,LightBlue) >> {
            unsigned int MaxWidth
            unsigned int MaxHeight
            unsigned int MaxNumMines
            bool IsFlagState
            ---
            + int main()
            + Difficulty PromptDifficulty()
            + void DisplayBoard(Board board)
            + void ParseCommands()
        }

        struct Difficulty {
            + unsigned int : Height
            + unsigned int : Width
            + unsigned int : NumMines
        }
        
        class Board {
            - unsigned int : Height
            - unsigned int : Width
            - unsigned int : NumMines
            - unsigned int : NumFlags
            - Cell[][] : cells
            ---
            + Board(Difficulty difficulty)
            + ~Board()
            + void ToggleFlagCell(unsigned int x, unsigned int y)
            + void RevealCell(unsigned int x, unsigned int y)
            + unsigned short int GetGameState()
            + Cell[][] GetCells()
        }
        
        class Cell {
            + bool : IsFlagged
            + bool : IsRevealed
            + bool : HasMine
            + unsigned short int : NumAdjacentMines
        }

    }

    @enduml
</details>

The plan is `Board` and `Cell` will use object oriented design whereas the GUI and the game state will all be in functional programming. Arguably `Cell` should be a struct too. I believe functional programming is more efficient, but I still wanted some experience with classes too. One benefit of using classes, is that I can use the resource acquisition is initialization (RAII) concept for the `cells` array. This concept will make memory management much easier. 

1. Gamplay loop: after a game finishes, another game is prompted until the user quits
2. Round loop: after the player makes a move, another move is prompted until a terminal state or the user quits
3. Flag loop: user can toggle between flagging mines and revealing mines