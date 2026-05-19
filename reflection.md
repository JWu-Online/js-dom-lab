# Reflection

1.  **`Array.isArray(divList)` returns `false` even though `divList` looks like an array.** Why is that, and which workaround did you use in TODO 2 (and why)?
    `divList` (or `statList` in this lab) is an `HTMLCollection` or `NodeList`, not a true JavaScript `Array`. These are array-like objects provided by the DOM API, meaning they have a `length` property and you can access elements by index, but they do not inherit methods like `forEach`, `map`, or `filter` from `Array.prototype`.
    In TODO 2, I used the spread operator (`...`) to convert the `HTMLCollection` into a real `Array`. This creates a new array containing all the elements from the `HTMLCollection`, allowing me to then use array methods like `forEach`.

2.  **What does `event.preventDefault()` do in TODO 5, and what happens if you forget it?** (Try removing it and see.)
    In TODO 5, `event.preventDefault()` stops the default behavior of a form submission, which is to reload the page. When a form is submitted, the browser typically sends an HTTP request to the server (or the current page if no action is specified) and reloads the page.
    If you forget `event.preventDefault()`, the page will reload every time the form is submitted. This would cause any dynamic changes made by JavaScript (like adding new recruits to the list) to be lost, and the user experience would be disrupted.

3.  **In TODO 4a you used `btn.dataset.member` instead of writing four separate event listeners.** Why is the `data-*` approach better as the app grows?
    The `data-*` attribute approach (`btn.dataset.member`) is better because it allows for a single, generic event listener to handle clicks on multiple similar elements. Instead of writing a separate event listener for each button (e.g., `domBtn.addEventListener(...)`, `brianBtn.addEventListener(...)`), we can attach one listener to all buttons with the `.switch-btn` class. The `data-member` attribute then provides the specific information (the member's key) needed to perform the correct action (`showMember(memberKey)`).
    As the app grows and you add more crew members, you only need to add a new button in the HTML with the appropriate `data-member` attribute. The JavaScript event handling code remains unchanged, making the code more scalable, maintainable, and less repetitive.

4.  **`.innerText` vs `.innerHTML` — when would you reach for each one?** Bonus: what's a security risk with putting user-typed text into `.innerHTML`?
    *   **`.innerText`**: Use `.innerText` when you want to set or get the plain, visible text content of an element, ignoring any HTML tags. It's generally safer and often preferred when dealing with text that shouldn't be interpreted as HTML.
    *   **`.innerHTML`**: Use `.innerHTML` when you need to set or get the HTML content (including tags) inside an element. This is useful for dynamically generating or replacing complex HTML structures.

    **Security Risk with `.innerHTML`**: A significant security risk with putting user-typed text directly into `.innerHTML` is Cross-Site Scripting (XSS). If a user inputs malicious script tags (e.g., `<script>alert('You've been hacked!')</script>`), and this input is then rendered using `.innerHTML`, the browser will execute that script. This can lead to session hijacking, data theft, or defacement of the website. To prevent this, user-provided content should always be sanitized or escaped before being inserted with `.innerHTML`, or preferably, use `.innerText` if only plain text is needed.
