## Directory Setup
```
rhythm/
- __init__.py
- assets/
    - default.json
- levels/
    - ... (JSON files)
- rhythm/
    - boxes.py (class) -> WASD boxes
    - display.py (class) -> manage environment
    - game.py (functions) -> manage game
    - menu.py (class) -> display menu
    - note_manager.py (classes) -> manage notes
    - object.py (class) -> represents a displayed object
```

## Import Logic
```
object.py
    > menu.py
    > boxes.py
    >   > display.py
    >   note_manager.py
            > game.py
```
- notes will be registered to `note_manager.py` from `game.py`

## File Contents
`assets/`
- `default.json`
```json
{
    "default_line": {
        // line data
    },
    "default_box": {
        // box data
    },
    "default_note": {
        // note data
    }
}
```
`levels/`
- `___.json`
```json
{
    // "appearance" optional; uses assets/default.json otherwise
    "appearance": {
        "line_data": {
            
        }, 
        "box_data": {
            
        }, 
        "note_data": {

        }
    }, "notes": [
        "w", "-", "-", "-", 
        "a", "-", "-", "-", 
        "s", "-", "-", "-", 
        "d", "-", "-", "-"
    ]
}
```
`rhythm/`
- `boxes.py`
    - `Box()` -> blueprint for boxes
        - `on('hit')` -> event handler when key is correctly pressed
        - `hit()` -> handles effects for when note is correctly pressed 
            - handle if a `hit()` is called while another `hit()` effect is running
- `display.py`
    - `Environment()` -> loads boxes, notes, and lines
    - `draw_box()` -> draws boxes
    - `draw_note()` -> draws notes
    - `draw_line()` -> draws lines
- `game.py`
    - `setup()` -> sets up game (initializes display, load classes, load levels)
    - `game()` -> runs the game (manage levels, display menu, read levels, register notes)
- `menu.py`
    - `Button()` -> blueprint for making a button
    - `Menu()` -> blueprint for making a menu
- `note_manager.py`
    - `Note()` -> blueprint for instantiating a note (from `Object()`)
    - `NoteManager()` -> manages all notes currently on-screen
- `object.py`
    - `Object()` -> represents a displayed object (will manage object's velocity on-screen, and all that stuff)


## Display Components
- W A S D boxes on the left (`rhythm/rhythm/boxes.py`)
    - when the correct key is pressed just as the letter is going over the WASD boxes (with a buffer of a few frames), have an effect play on that box (effects logic included in `boxes.py`)
- moving letters from the right to the left (the "notes")
    - if not correctly pressed, the note will stop on the left, turn red, and fall downwards, off-screen
    - if correctly pressed, the note will slowly dissipate, floating over the corresponding box
    - notes will have a mode (moving right, correctly pressed, or incorrectly pressed), that will dictate their motion and appearance in the next frame
- horizontal lines extending from the right of the screen to the boxes (`rhythm/rhythm/display.py`)

## Tasks
- Environment
    - Implement drawing features
- W A S D boxes
    - Draw boxes
        - Implement `Box()` class
    - Store box display data
- Moving Letters
    - Draw letters
    - Store letters display data
    - Implement movement (`Object()`)
    - Implement management of appearing and disappearing (that is, adding to and removing from `Environment()`)
    - Implement `Box().on('hit')`
- Horizontal Lines
    - Implement drawing
    - Store lines display data