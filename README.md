# anime-tracker-c
# TV/Anime Tracker

A command-line tracker for TV shows and anime, written in C.

Built entirely on an Android phone (Vivo T2) using [Termux](https://termux.dev/) — no laptop, no IDE. `nano` for editing, `clang` for compiling.

## Features

- Add a show (title, status, episodes watched, rating)
- List all shows
- Edit an existing show
- Delete a show
- Saves to `shows.txt` so your list persists between runs

## Building and running

Works on Linux, macOS, or in Termux on Android.

```bash
clang tracker.c -o tracker
./tracker
```

(`gcc` works too if you don't have clang.)

## Usage

Run the program and pick an option from the menu:

```
press 1 to add show to the list
press 2 to see list of shows
press 3 to exit
press 4 to edit a show
press 5 to delete a show
```

Shows are saved automatically to `shows.txt` in the same directory after every add, edit, or delete.

## What I learned building this

This was a project for learning core C concepts hands-on:

- **Structs** — grouping a show's title, status, episodes watched, and rating into one `Show` type
- **Arrays of structs** — storing the whole list in a fixed-size array (`MAX_SHOWS`) with a running count
- **scanf formatting** — using `%99[^\n]` to read a full title with spaces, and `&` to pass addresses for numeric fields
- **File I/O** — `fopen`/`fclose`, writing with `fprintf`, reading back with `fscanf` until EOF
- **Array manipulation** — deleting an entry by shifting every later element down one slot, then decrementing the count
- **1-based vs 0-based indexing** — the menu shows shows as 1, 2, 3..., but the array needs index 0, 1, 2..., so user input is always adjusted with `pick - 1`
- **Debugging compiler errors** — chasing down a missing semicolon and a missing closing brace by reading clang's error output top to bottom

## Roadmap

- [ ] Validate empty title input on add
- [ ] Search by title
- [ ] Sort by rating
- [ ] Add a type field (TV / Anime / Movie)

## License

MIT — feel free to use or fork this for your own learning.
