# 📚 Book Nook — Book Tracker

Book Nook is a simple, user-friendly web application that helps you organize your personal reading list. Add books, track your reading progress, search your library, and manage your books in one place.

## ✨ Features

- **Add Books:** Add a book with its title and author.
- **Track Reading Status:** Organize books into three categories:
  - To read
  - Reading
  - Finished
- **Search Books:** Quickly find books by title or author.
- **Filter Your Library:** View all books or filter by reading status.
- **Reading Statistics:** See your total books, books currently being read, and finished books.
- **Update Book Status:** Change a book’s status whenever your reading progress changes.
- **Delete Books:** Remove books from your library when needed.
- **Form Validation:** Get helpful messages when required information is missing.
- **Automatic Local Storage:** Your book list is saved in your browser, so it remains available after refreshing the page in the same browser.
- **Responsive Design:** Use the application on desktop, tablet, and mobile screens.

## 🛠️ Technologies Used

- HTML5
- CSS3
- JavaScript
- Browser Local Storage
- Visual Studio Code
- Git and GitHub

## 📋 Requirements

Before running the project, make sure you have:

1. [Visual Studio Code](https://code.visualstudio.com/)
2. [Git for Windows](https://git-scm.com/install/windows)
3. A modern web browser, such as Chrome, Edge, or Firefox

## 🚀 How to Open the Project in VS Code

### Step 1: Open the Terminal

Open Visual Studio Code, then select **Terminal → New Terminal** from the menu.

### Step 2: Check Git Installation

Run:

```powershell
git --version
```

If a Git version appears, continue to the next step. If Git is not recognized, install it from [Git for Windows](https://git-scm.com/install/windows), then restart VS Code.

### Step 3: Clone the GitHub Repository

If you have not downloaded the repository to your computer, run:

```powershell
cd $HOME
git clone https://github.com/rthhhyy/kottayam-mini-project.git
```

### Step 4: Enter the Project Folder

```powershell
cd kottayam-mini-project
```

### Step 5: Open the Project in VS Code

```powershell
code .
```

If `code .` is not recognized, open VS Code and select **File → Open Folder**, then choose the `kottayam-mini-project` folder.

## ▶️ How to Run the Website

### Option 1: Open Directly in Your Browser

In the VS Code terminal, make sure you are inside the project folder, then run:

```powershell
start index.html
```

This opens the website in your default browser.

### Option 2: Run Using a Local Server

If Python is installed, run:

```powershell
python -m http.server 8000
```

Then open this address in your browser:

http://localhost:8000

To stop the server, return to the terminal and press **Ctrl + C**.

## 📁 Project Structure

Make sure the following files are in the same project folder:

```text
kottayam-mini-project/
├── index.html
├── style.css
├── app.js
├── README.md
└── PROMPTS.md
```

- `index.html` — Contains the webpage structure.
- `style.css` — Controls the design, colors, layout, and responsive styling.
- `app.js` — Handles adding, searching, filtering, updating, deleting, and saving books.
- `README.md` — Provides project information and setup instructions.
- `PROMPTS.md` — Documents development prompts and manual testing steps.

**Important:** The website will not display correctly if `style.css` or `app.js` is missing or saved under a different filename. Make sure all required files are present in the same folder.

## 💾 How Book Data Is Saved

Book Nook uses your browser's Local Storage to save your reading list. Data is stored locally in the browser on your computer.

- Refreshing the page does not normally remove your saved books.
- Your books are not automatically synced between different browsers or computers.
- Clearing the browser's site data may delete your saved books.

## 🧪 Basic Testing Checklist

- Add a book with a title and author.
- Try submitting the form with a missing title or author.
- Search for a book by title and author.
- Filter books by reading status.
- Change a book's status and check the statistics.
- Delete a book and verify the updated list.
- Refresh the page and confirm that saved books remain.

## 🎯 Project Goal

The goal of Book Nook is to provide a simple and attractive way to maintain a personal reading list, monitor reading progress, and encourage consistent reading habits.

## 👨‍💻 Author

Developed as a mini project using HTML, CSS, and JavaScript.
## 🧪 Testing Results

- ✅ Add books with a title and author.
- ✅ Validate missing title or author.
- ✅ Search books by title and author.
- ✅ Filter books by reading status.
- ✅ Update a book's reading status.
- ✅ Verify reading statistics update correctly.
- ✅ Delete books from the library.
- ✅ Reload the browser and confirm saved books remain visible.
- ✅ Confirm updated reading statuses persist after reloading.
- ✅ Verify the application works as expected.

**Result:** All listed manual tests passed successfully.
