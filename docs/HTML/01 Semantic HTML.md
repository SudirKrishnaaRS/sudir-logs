# Semantic HTML

## Definition

Semantic HTML uses elements that have meaningful names describing their purpose, improving the structure and accessibility of a webpage.

![image](https://github.com/user-attachments/assets/711bb61c-1df0-4d07-8b77-f25081c9480c)

## Common Semantic Tags

- **`<header>`**: Represents the introductory section of a page or a section.
- **`<nav>`**: Defines a navigation block for links.
- **`<main>`**: Represents the main content unique to the document.
- **`<section>`**: Groups related content, often with a heading.
- **`<article>`**: Represents independent, self-contained content.
- **`<aside>`**: Used for content indirectly related to the main content (e.g., sidebars).
- **`<footer>`**: Represents the footer of a document or a section.
- **`<figure>`** and **`<figcaption>`**: Used for images or other media with a caption.
- **`<mark>`**: Highlights text for relevance or context.
- **`<time>`**: Represents a specific time or date.

## Benefits

1. **Accessibility**: Helps screen readers and other assistive technologies.
2. **SEO**: Improves search engine ranking by providing clear content structure.
3. **Maintainability**: Easier to understand and maintain code.

## Gotchas

- Avoid non-semantic tags like `<div>` or `<span>` unless necessary.
- Use semantic tags in the right context (e.g., `<section>` needs a heading).
- Combine with ARIA roles where needed, but avoid redundancy (e.g., don't add `role="navigation"` to `<nav>`).

## Example Code

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <title>Semantic HTML Example</title>
  </head>
  <body>
    <header>
      <h1>My Blog</h1>
      <nav>
        <ul>
          <li><a href="#home">Home</a></li>
          <li><a href="#about">About</a></li>
        </ul>
      </nav>
    </header>
    <main>
      <article>
        <h2>Post Title</h2>
        <p>This is a blog post about semantic HTML.</p>
      </article>
    </main>
    <footer>
      <p>&copy; 2024 My Blog</p>
    </footer>
  </body>
</html>
```

### Code Output

![image](https://github.com/user-attachments/assets/d250c56a-22bd-4460-a92a-be6f952cadad)

## Common Interview Questions and Answers

1. **Why is semantic HTML important?**  
   Semantic HTML makes webpages more accessible, improves SEO, and creates cleaner, more maintainable code. It provides meaningful structure, enabling browsers, assistive technologies, and developers to understand content better.

2. **What is the difference between `<section>` and `<div>`?**

   - **`<section>`**: Represents a thematic grouping of content with a heading, implying context and meaning.
   - **`<div>`**: A generic container with no semantic meaning, used mainly for styling or scripting.

3. **Explain the role of `<header>` and `<footer>` in a webpage.**

   - **`<header>`**: Typically contains introductory content or navigation links for a page or section.
   - **`<footer>`**: Contains information about the enclosing content, such as copyright, links, or contact information.

4. **How does semantic HTML improve SEO?**  
   Search engines understand the structure of semantic tags better, making it easier to index content. For example, `<article>` indicates primary content, while `<nav>` signals important navigation links.

5. **What are the accessibility benefits of using `<nav>` or `<main>`?**  
   Screen readers can identify `<nav>` as the navigation region and `<main>` as the primary content, allowing users to navigate pages efficiently without unnecessary repetition.
