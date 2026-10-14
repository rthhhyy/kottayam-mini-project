
'use strict';

(() => {
  const STORAGE_KEY = 'book-nook-books-v1';

  const VALID_STATUSES = ['To read', 'Reading', 'Finished'];

  const COVER_CLASSES = [
    'cover-1',
    'cover-2',
    'cover-3',
    'cover-4'
  ];

  const STATUS_CLASSES = {
    'To read': 'status-todo',
    'Reading': 'status-reading',
    'Finished': 'status-finished'
  };

  const $ = (selector) => document.querySelector(selector);

  const elements = {
    form: $('#book-form'),
    title: $('#title'),
    author: $('#author'),
    status: $('#status'),
    titleError: $('#title-error'),
    authorError: $('#author-error'),

    totalCount: $('#total-count'),
    readingCount: $('#reading-count'),
    finishedCount: $('#finished-count'),

    search: $('#search'),
    visibleCount: $('#visible-count'),
    bookList: $('#book-list'),
    emptyState: $('#empty-state'),
    emptyTitle: $('#empty-title'),
    emptyCopy: $('#empty-copy'),
    emptyAdd: $('#empty-add'),

    toast: $('#toast'),

    filters: [...document.querySelectorAll('[data-filter]')],

    filterCounts: {
      All: $('#all-count'),
      'To read': $('#todo-count'),
      Reading: $('#reading-filter-count'),
      Finished: $('#finished-filter-count')
    }
  };

  let books = loadBooks();
  let activeFilter = 'All';
  let toastTimeout = null;

  // Return saved books, or start with an empty library.
  function loadBooks() {
    try {
      const saved = localStorage.getItem(STORAGE_KEY);

      if (!saved) {
        return [];
      }

      const parsed = JSON.parse(saved);

      if (!Array.isArray(parsed)) {
        return [];
      }

      return parsed
        .filter((book) => {
          return (
            book &&
            typeof book.id === 'string' &&
            typeof book.title === 'string' &&
            typeof book.author === 'string' &&
            VALID_STATUSES.includes(book.status)
          );
        })
        .map((book) => ({
          id: book.id,
          title: book.title.trim(),
          author: book.author.trim(),
          status: book.status,
          createdAt: Number.isFinite(book.createdAt)
            ? book.createdAt
            : 0
        }))
        .filter((book) => book.title && book.author)
        .sort((a, b) => b.createdAt - a.createdAt);
    } catch (error) {
      console.error('Could not load saved books:', error);
      return [];
    }
  }

  // Save changes without breaking the rest of the app if storage is unavailable.
  function saveBooks() {
    try {
      localStorage.setItem(STORAGE_KEY, JSON.stringify(books));
      return true;
    } catch (error) {
      console.error('Could not save books:', error);
      showToast('Could not save changes. Check your browser storage.');
      return false;
    }
  }

  function createId() {
    if (
      typeof crypto !== 'undefined' &&
      typeof crypto.randomUUID === 'function'
    ) {
      return crypto.randomUUID();
    }

    return `${Date.now()}-${Math.random().toString(36).slice(2)}`;
  }

  function normalizeText(value) {
    return value.trim().toLocaleLowerCase();
  }

  function setFieldError(input, errorElement, message) {
    errorElement.textContent = message;
    input.setAttribute('aria-invalid', message ? 'true' : 'false');

    if (message) {
      input.setAttribute(
        'aria-describedby',
        errorElement.id
      );
    } else {
      input.removeAttribute('aria-describedby');
    }
  }

  function clearErrors() {
    setFieldError(elements.title, elements.titleError, '');
    setFieldError(elements.author, elements.authorError, '');
  }

  function validateForm() {
    const title = elements.title.value.trim();
    const author = elements.author.value.trim();

    setFieldError(
      elements.title,
      elements.titleError,
      title ? '' : 'Please enter a title'
    );

    setFieldError(
      elements.author,
      elements.authorError,
      author ? '' : 'Please enter an author'
    );

    if (!title) {
      elements.title.focus();
      return false;
    }

    if (!author) {
      elements.author.focus();
      return false;
    }

    return true;
  }

  function showToast(message) {
    if (!elements.toast) {
      return;
    }

    window.clearTimeout(toastTimeout);

    elements.toast.textContent = message;
    elements.toast.hidden = false;
    elements.toast.setAttribute('role', 'status');
    elements.toast.setAttribute('aria-live', 'polite');

    toastTimeout = window.setTimeout(() => {
      elements.toast.hidden = true;
    }, 3000);
  }

  function getStatusCounts() {
    return {
      All: books.length,
      'To read': books.filter((book) => book.status === 'To read').length,
      Reading: books.filter((book) => book.status === 'Reading').length,
      Finished: books.filter((book) => book.status === 'Finished').length
    };
  }

  function updateCounts() {
    const counts = getStatusCounts();

    elements.totalCount.textContent = String(counts.All);
    elements.readingCount.textContent = String(counts.Reading);
    elements.finishedCount.textContent = String(counts.Finished);

    Object.entries(elements.filterCounts).forEach(([status, element]) => {
      if (element) {
        element.textContent = String(counts[status]);
      }
    });
  }

  function getFilteredBooks() {
    const query = normalizeText(elements.search.value);

    return books
      .filter((book) => {
        const matchesStatus =
          activeFilter === 'All' || book.status === activeFilter;

        const matchesSearch =
          !query ||
          normalizeText(book.title).includes(query) ||
          normalizeText(book.author).includes(query);

        return matchesStatus && matchesSearch;
      })
      .sort((a, b) => b.createdAt - a.createdAt);
  }

  function createElement(tagName, className, text) {
    const element = document.createElement(tagName);

    if (className) {
      element.className = className;
    }

    if (text !== undefined) {
      element.textContent = text;
    }

    return element;
  }

  function createBookCard(book, index) {
    const card = createElement('article', 'book-card');
    const cover = createElement(
      'div',
      `book-cover ${COVER_CLASSES[index % COVER_CLASSES.length]}`,
      '📖'
    );

    cover.setAttribute('aria-hidden', 'true');

    const info = createElement('div', 'book-info');
    const title = createElement('h3', '', book.title);
    const author = createElement(
      'p',
      'book-author',
      `by ${book.author}`
    );

    const meta = createElement('div', 'book-meta');
    const statusBadge = createElement(
      'span',
      `status ${STATUS_CLASSES[book.status]}`,
      book.status
    );

    meta.append(statusBadge);
    info.append(title, author, meta);

    const actions = createElement('div', 'book-actions');

    const statusLabel = createElement(
      'label',
      '',
      'Reading status'
    );
    statusLabel.className = 'visually-hidden';

    const statusSelect = document.createElement('select');
    statusSelect.className = 'status-select';
    statusSelect.setAttribute(
      'aria-label',
      `Reading status for ${book.title}`
    );

    VALID_STATUSES.forEach((status) => {
      const option = document.createElement('option');
      option.value = status;
      option.textContent = status;
      option.selected = status === book.status;
      statusSelect.append(option);
    });

    statusSelect.addEventListener('change', () => {
      updateBookStatus(book.id, statusSelect.value);
    });

    const deleteButton = createElement(
      'button',
      'delete-btn',
      'Delete'
    );

    deleteButton.type = 'button';
    deleteButton.setAttribute(
      'aria-label',
      `Delete ${book.title}`
    );

    deleteButton.addEventListener('click', () => {
      deleteBook(book.id);
    });

    actions.append(statusSelect, deleteButton);
    card.append(cover, info, actions);

    return card;
  }

  function updateEmptyState() {
    const hasBooks = books.length > 0;
    const hasVisibleBooks = elements.bookList.children.length > 0;
    const query = elements.search.value.trim();

    elements.emptyState.hidden = hasVisibleBooks;

    if (hasVisibleBooks) {
      return;
    }

    if (!hasBooks) {
      elements.emptyTitle.textContent = 'Your shelf is waiting';
      elements.emptyCopy.textContent =
        'Add your first book and start building your reading list.';
    } else if (query) {
      elements.emptyTitle.textContent = 'No matching books';
      elements.emptyCopy.textContent =
        'Try a different title or author, or clear your search.';
    } else {
      elements.emptyTitle.textContent = 'Nothing in this section yet';
      elements.emptyCopy.textContent =
        activeFilter === 'Finished'
          ? 'Books you finish will appear here.'
          : activeFilter === 'Reading'
            ? 'Update a book to Reading to see it here.'
            : 'Try another status filter to find your books.';
    }

    if (elements.emptyAdd) {
      elements.emptyAdd.textContent = hasBooks
        ? 'Add another book'
        : 'Add your first book';
    }
  }

  function renderBooks() {
    const filteredBooks = getFilteredBooks();
    const fragment = document.createDocumentFragment();

    filteredBooks.forEach((book, index) => {
      fragment.append(createBookCard(book, index));
    });

    elements.bookList.replaceChildren(fragment);
    elements.visibleCount.textContent = String(filteredBooks.length);

    updateCounts();
    updateEmptyState();
    updateFilterButtons();
  }

  function updateFilterButtons() {
    elements.filters.forEach((button) => {
      const isActive = button.dataset.filter === activeFilter;

      button.classList.toggle('active', isActive);
      button.setAttribute('aria-pressed', String(isActive));
    });
  }

  function addBook(event) {
    event.preventDefault();
    clearErrors();

    if (!validateForm()) {
      return;
    }

    const title = elements.title.value.trim();
    const author = elements.author.value.trim();
    const status = elements.status.value;

    if (!VALID_STATUSES.includes(status)) {
      showToast('Please choose a valid reading status.');
      elements.status.focus();
      return;
    }

    const book = {
      id: createId(),
      title,
      author,
      status,
      createdAt: Date.now()
    };

    books.unshift(book);

    if (!saveBooks()) {
      books.shift();
      return;
    }

    // Show the newly added book immediately.
    activeFilter = 'All';
    elements.search.value = '';
    elements.form.reset();
    clearErrors();

    renderBooks();
    elements.title.focus();
    showToast(`“${title}” added to your shelf.`);
  }

  function updateBookStatus(bookId, newStatus) {
    if (!VALID_STATUSES.includes(newStatus)) {
      showToast('Please choose a valid reading status.');
      return;
    }

    const book = books.find((item) => item.id === bookId);

    if (!book || book.status === newStatus) {
      return;
    }

    const previousStatus = book.status;
    book.status = newStatus;

    if (!saveBooks()) {
      book.status = previousStatus;
      renderBooks();
      return;
    }

    renderBooks();
    showToast(`Reading status changed to “${newStatus}”.`);
  }

  function deleteBook(bookId) {
    const index = books.findIndex((book) => book.id === bookId);

    if (index === -1) {
      return;
    }

    const [removedBook] = books.splice(index, 1);

    if (!saveBooks()) {
      books.splice(index, 0, removedBook);
      renderBooks();
      return;
    }

    renderBooks();
    showToast(`“${removedBook.title}” removed from your shelf.`);
  }

  function handleFilterClick(event) {
    const button = event.target.closest('[data-filter]');

    if (!button || !elements.bookList) {
      return;
    }

    const requestedFilter = button.dataset.filter;

    if (requestedFilter !== 'All' &&
        !VALID_STATUSES.includes(requestedFilter)) {
      return;
    }

    activeFilter = requestedFilter;
    renderBooks();
  }

  function handleSearchInput() {
    renderBooks();
  }

  function handleFormInput(event) {
    if (event.target === elements.title && elements.title.value.trim()) {
      setFieldError(elements.title, elements.titleError, '');
    }

    if (event.target === elements.author &&
        elements.author.value.trim()) {
      setFieldError(elements.author, elements.authorError, '');
    }
  }

  function handleEmptyAdd() {
    elements.title.focus();

    const formTop = elements.form.getBoundingClientRect().top +
      window.scrollY;

    window.scrollTo({
      top: Math.max(0, formTop - 24),
      behavior: window.matchMedia('(prefers-reduced-motion: reduce)').matches
        ? 'auto'
        : 'smooth'
    });
  }

  function initialize() {
    elements.form.addEventListener('submit', addBook);
    elements.form.addEventListener('input', handleFormInput);

    elements.search.addEventListener('input', handleSearchInput);

    elements.filters.forEach((button) => {
      button.addEventListener('click', handleFilterClick);
    });

    if (elements.emptyAdd) {
      elements.emptyAdd.addEventListener('click', handleEmptyAdd);
    }

    renderBooks();
  }

  initialize();
})();
