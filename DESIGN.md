# FrostyTerminal Design Guidelines

This document outlines the strict design choices and constraints for the FrostyTerminal project. Future changes must adhere to these guidelines to maintain the retro aesthetic and functional logic.

## 1. Functional Overview
**FrostyTerminal** is a static, retro-styled message viewer designed to emulate an old-school computer terminal.
*   **Goal**: To display a series of text-based messages and ASCII art in a highly stylized, immersive environment.
*   **Interaction Model**:
    *   **Index Page**: Acts as the central directory. Users see a grid of message IDs (e.g., `0001`, `0002`) and click one to enter.
    *   **Message Pages**: Display static content. Users read the message and use the fixed navigation bar to proceed.
    *   **Navigation**:
        *   **`<<` (Back)**: Moves to the previous message.
        *   **`>>` (Next)**: Moves to the next message.
        *   **`☼` (Random)**: Instantly jumps to a random message.
*   **User Experience**: The site feels rigid and mechanical. Content does not "flow" dynamically; it is presented in fixed "screens" or "pages".

## 2. Core Aesthetic
*   **Theme**: Retro VGA terminal style.
*   **Colors**:
    *   **Background**: Pure Black (`#000000`).
    *   **Text**: White at **80% opacity** (`rgba(255, 255, 255, 0.8)`).
    *   **Buttons (Default)**: White at **20% opacity** (`rgba(255, 255, 255, 0.2)`).
    *   **Buttons (Disabled)**: White at **10% opacity** (`rgba(255, 255, 255, 0.1)`).
    *   **Buttons (Hover)**: Brighten to text color (80% white).
*   **Visual Effects**:
    *   **Scanlines**: A CSS `linear-gradient` overlay is applied to the body to simulate a CRT screen.
    *   **Cursor**: A blinking underscore (`_`) or `span.cursor` must appear at the very end of the content.
    *   **No Borders**: Navigation buttons and links must **never** have borders.

## 3. Typography
*   **Primary Font**: `Web437_IBM_VGA_8x16` (Local `.woff` file). This is the defining look of the terminal.
*   **Multilingual Support**:
    *   **Japanese/Chinese**: `DotGothic16` (Google Fonts).
    *   **Korean**: `NeoDunggeunmo` (CDN).
    *   **Fallback**: `VT323`, `monospace`.
*   **Constraint**: The Index page message grid **must** use the IBM font stack, not generic monospace.

## 4. Layout & Structure
*   **Single Strip Flow**:
    *   Do **not** use rigid wrapper divs (like `.ascii-art` or `.message-content`) to separate content.
    *   **Top Spacing**: Use exactly **6 `<br>` tags** at the top of the `.container` to reserve space (~200px) for optional ASCII art.
*   **Navigation Bar**:
    *   **Position**: Fixed to the bottom center of the screen (`bottom: 3rem`).
    *   **Button Order**: `<<` (Back) &nbsp; `☼` (Random) &nbsp; `>>` (Next).
    *   **Random Icon**: Use the sun symbol **`☼`** (U+263C).
    *   **Stability**: The navigation bar must **never move** based on content length.
    *   **Disabled State**: Disabled buttons (e.g., "Next" on the last message) must remain **visible** (10% opacity) to preserve the layout's center of gravity.

## 5. Index Page (Directory)
*   **Message Grid**: Links are displayed in a **4-column grid** (`.message-grid`).
*   **Link Style**:
    *   Format: `0001`, `0002`, etc.
    *   **No Underline**: Links must not have text decoration.
    *   **Font**: Must use the primary IBM font.
*   **Navigation**: The `<<` and `>>` buttons are present but **disabled** (10% opacity). The `☼` button remains active.

## 6. Technical Constraints
*   **Static Site**: The project is hosted on GitHub Pages.
*   **JavaScript**: Kept to an absolute minimum (only for the random button logic).
*   **File Structure**:
    *   `index.html`: Main directory.
    *   `messages/`: Folder containing individual `001.html`, `002.html`, etc.
    *   `style.css`: Global stylesheet.
