# anime-tracker-c
# TV/Anime Tracker

A command-line tracker for TV shows and anime, written in C.

Built entirely on an Android phone (Vivo T2) using [Termux](https://termux.dev/) — no laptop, no IDE. `nano` for editing, `clang` for compiling.

## Features

- Add a show (title, status, episodes watched, rating)
- List all shows
- Edit an existing show
- Delete a show
- Search shows by title (partial match)
- Filter shows by status
- Export your list to a clean, readable `my_showList.txt`
- Dynamic list — grows automatically as you add more shows, no fixed cap
- Saves to `shows.txt` so your list persists between runs
- Status messages ("Show added!", "Invalid number!", etc.) shown at the top of the menu after each action

## Building and running

Works on Linux, macOS, or in Termux on Android.

```bash
clang tracker.c -o tracker
./tracker
```

(`gcc` works too if you don't have clang.)

> Note: `system("clear")` is Linux/macOS-specific. On Windows, swap it for `system("cls")`.

## Usage

Run the program and pick an option from the menu:

```
press 1 to add show to the list
press 2 to see list of shows
press 3 to exit
press 4 to edit a show
press 5 to delete a show
press 6 to search by title
press 7 to search by status
press 8 to export list
```

Shows are saved automatically to `shows.txt` in the same directory after every add, edit, or delete. Use option 8 to write a formatted copy to `my_showList.txt`.

## What I learned building this

This was a project for learning core C concepts hands-on:

- **Structs** — grouping a show's title, status, episodes watched, and rating into one `Show` type
- **Dynamic arrays** — replaced the original fixed-size `MAX_SHOWS` array with a `Show *library` pointer that grows via `realloc`, doubling capacity whenever it fills up (`ensure_capacity()`)
- **Memory management** — `realloc` to grow storage on demand, and `free(library)` before the program exits
- **scanf formatting** — using `%99[^\n]` to read a full title with spaces, and `&` to pass addresses for numeric fields
- **File I/O** — `fopen`/`fclose`, writing with `fprintf`, reading back with `fscanf` until EOF
- **Array manipulation** — deleting an entry by shifting every later element down one slot, then decrementing the count
- **1-based vs 0-based indexing** — the menu shows shows as 1, 2, 3..., but the array needs index 0, 1, 2..., so user input is always adjusted with `pick - 1`
- **String functions** — `strstr` for partial-match search, `strcmp` for exact status filtering, `strcpy` for copying status messages into a buffer
- **Variable scope** — why the `message` buffer lives in `main()` and gets filled by the switch cases rather than from inside helper functions
- **A simple message system** — storing a result string in `main()` and displaying it at the top of the next screen, instead of printing it immediately and losing it on the next `clear`
- **Input buffer handling** — a `clear_stdin()` helper to flush leftover input after `scanf`, and a `wait_for_enter()` helper to pause the screen until the user is ready to continue
- **Debugging compiler errors** — chasing down a missing semicolon and a missing closing brace by reading clang's error output top to bottom

## Roadmap

- [x] Search by title
- [x] Filter by status
- [x] Export list to a file
- [x] Switch from a fixed-size array to a dynamic one
- [ ] Color output (cyan headers, green/yellow/red ratings)
- [ ] Sort by rating (`qsort`)
- [ ] Add a type field (TV / Anime / Movie)

## License

MIT — feel free to use or fork this for your own learning.

