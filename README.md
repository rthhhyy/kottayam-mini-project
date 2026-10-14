
# 📚 Book Nook — My Reading Tracker

A simple, responsive web app for organizing the books you want to read, are currently reading, or have finished.

Book Nook is built with plain HTML, CSS, and JavaScript. No frameworks, database, or build tools are required.

## ✨ Features

- **Add books:** Enter a book title, author, and reading status.
- **Input validation:** Title and author are required, with clear error messages.
- **Reading statuses:** Organize books into To read, Reading, and Finished.
- **Search:** Find books by title or author with case-insensitive matching.
- **Status filters:** View all books or filter by reading status.
- **Live statistics:** See your total books, currently reading books, and finished books.
- **Persistent storage:** Automatically save your library in the browser using `localStorage`.
- **Delete books:** Remove books from your reading list.
- **Newest first:** Newly added books appear at the top of the list.
- **Responsive design:** Use the app on desktop, tablet, and mobile screens.
- **Accessible feedback:** Form errors and status notifications help users understand their actions.

## 🛠️ Built With

- HTML5 — page structure and form elements
- CSS3 — styling, responsive layouts, and visual effects
- Vanilla JavaScript — app logic, search, filtering, and data management
- Browser `localStorage` — saving books between visits
- Google Fonts — DM Sans and Playfair Display

## 📁 Project Structure

```text
kottayam-mini-project/
├── index.html    # Main page and book form
├── style.css     # Layout, colors, and responsive styling
├── app.js        # Book management and localStorage
├── README.md     # Project documentation
└── PROMPTS.md    # Development prompts and testing log
```

## 🚀 Getting Started

### Option 1: Run locally

1. Clone or download this repository.
2. Make sure `index.html`, `style.css`, and `app.js` are in the same folder.
3. Open `index.html` in a modern web browser.

```bash
git clone https://github.com/rthhhyy/kottayam-mini-project.git
cd kottayam-mini-project
```

Then open `index.html` in your browser.

### Option 2: Use VS Code

1. Open the project folder in Visual Studio Code.
2. Open `index.html`.
3. Run it with a local development server, such as the Live Server extension.

A local server is recommended for consistent browser behavior, but no compilation or package installation is needed.

### Option 3: Publish with GitHub Pages

1. Open the repository on GitHub.
2. Go to **Settings → Pages**.
3. Under the build and deployment section, choose **Deploy from a branch**.
4. Select your default branch (usually `main`) and the root folder (`/`).
5. Save the settings and wait for deployment.
6. Open the published URL shown in the Pages settings.

Ensure that `index.html`, `style.css`, and `app.js` are committed to the selected branch.

## 📖 How to Use

1. Enter a book title.
2. Enter the author's name.
3. Choose a reading status.
4. Click **Add book**.
5. Use the search box to find books by title or author.
6. Select a status filter to narrow down your library.
7. Change a book's status as you make progress.
8. Delete books you no longer want to track.

Your statistics update as books are added, updated, or deleted.

## 💾 How Data Is Stored

Book Nook uses the browser's `localStorage` API to save the book list under this key:

```text
book-nook-books-v1
```

The stored data includes each book's:

- Unique ID
- Title
- Author
- Reading status
- Creation timestamp

### Important storage details

- Data remains available after refreshing or reopening the app in the same browser profile.
- Data is local to the browser and site origin. It does not automatically sync across devices or browsers.
- Clearing site data or browser storage can delete your saved books.
- Opening the app under a different origin, hostname, or port creates a separate storage area.
- The app does not require a user account or send book data to a backend server.
- If browser storage is unavailable or full, saving changes may fail and the app will show an error notification.

## 🧪 Manual Testing Checklist

Use the following checklist to verify the main features.

| Test | Action | Expected result |
|---|---|---|
| Empty form | Submit without a title or author | Required-field errors appear |
| Add a book | Enter a title and author, then submit | The book appears in the list |
| Default status | Add a book using the default status | It appears under To read |
| Newest first | Add two books one after the other | The newest book appears first |
| Search by title | Search for part of a title | Matching books appear |
| Search by author | Search for an author's name | Matching books appear |
| Case-insensitive search | Search using different capitalization | The same matching books appear |
| Filter by status | Select Reading or Finished | Only books with that status appear |
| Update status | Change a book's status | Its status and statistics update |
| Delete a book | Click Delete on a book | The book disappears and counts update |
| Persist data | Add a book and refresh the page | The saved book remains visible |
| Empty state | Search for a nonexistent book | A no-matching-books message appears |
| Mobile layout | Open the app at a narrow viewport | Form and book cards adapt to the screen |

## 🔧 Troubleshooting

### Books disappear after refreshing

- Check that browser storage is enabled.
- Make sure you are using the same browser profile and site origin.
- Check the browser console for storage-related errors.

### CSS or JavaScript changes do not appear

- Confirm the filenames are exactly `style.css` and `app.js`.
- Confirm `index.html` references both files correctly.
- Refresh the page or clear the browser cache if necessary.
- Check the browser developer console for errors.

### Search returns no results

- Clear the search field and try again.
- Check that the title or author is spelled correctly.
- Select **All** to remove status filtering.

## 🔒 Privacy

This project has no backend, login system, or external database. Book information is stored locally in the browser through `localStorage`.

Google Fonts may require an internet connection to load the chosen fonts. The app's core functionality does not require a third-party JavaScript library.

## 🌱 Future Improvements

Possible enhancements include:

- Book cover images
- Reading goals and progress tracking
- Sorting by title or author
- Exporting and importing a book list
- Optional cloud synchronization
- Automated tests

## 📄 License

This project is intended as a small learning project. Add a license file if you plan to distribute or reuse it under specific terms.

---

Made with 📚 and a love of reading.
