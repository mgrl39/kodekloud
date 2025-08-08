# Linux vi Editor
**Learn to se the vi editor in Linux.**

[LINK](https://studio.kodekloud.com/labs/linux/linux-vi-editor) - 08/08/2025 - 15minutes
## Exercises
### What is the default editor configured in lab?
In this case -> `vim`
### What is the command for the `vim` text editor to open a file?
`vi` or `vim`

### What are the operation modes in `vi editor`
All are correct: `Command Mode`, `Insert Mode`, `Last Line`
### What is the default mode of the editor after opening a file by `vi editor`?
`Command Mode`
### Identify the wrong statement below while switching operation modes in the editor.
`Press capital letter T to switch to insert mode from command mode`
### Identify the correct statement from the below exit commands.
All are correct:  `q! - Quit vi and do not save changes.`, `wq - Save and quit/exit vi`, `w - Save and continue editing.`
### Task -1
1. Open a file by "vi kodekloud.txt" and an editor will be in default operation mode (`command mode`).
2. Press lowercase `i` to enter into `insert mode`.
3. Type `Hello world!`.
4. Press `Esc` button to return to the **command** mode.
5. Press `wq!` to save the file and exit the editor.
### What is the command to `copy a line` in vi editor?
`yy`
### Identify the wron statement for commands we use in vi editor.
`dd - Highlight a line`
### Identify the option with the correct actions matched to the command in the vi editor.
- A. u - undo the change
- B. ctrl + r - redo the change
- C. ctrl + y - redo the change
- D. ctrl + x - undo the change

`A and B`
### Open the file located at `/home/bob/testfile.txt` using the vi editor. Then, move the line currently located at line number 9 to position it at line number 5.
```bash
vi /home/bob/testfile.txt
:9
dd
:4
p
wq
```
### Delete the first three lines in `/home/bob/testfile.txt`
```
vi /home/bob/testfile.txt
:0d3
:wq!
```
