---
marp: true
theme: gaia
class: invert
paginate: true
---

# SDEV153 - Lecture 3

Website Design Principles & Mobile First Design

---

## Why do we Design Websites?

We design in the process of shaping content so users can understand, trust, and use a websites with minimal effort.

Making a website visually appealing helps build user trust and credibility.

Making a website easy to navigate, view on different devices, and find information makes it more likely users will stay and return.

---

## Design Principles for building Visually Appealing Websites

- **Hierarchy** - Use size, color, and placement to indicate importance
- **Repetition** - Repeat design elements to create consistency
- **Color** - Color theory and psychology to evoke emotions and convey messages
- **Contrast** - Use contrasting colors and fonts to make elements stand out

---

## How do we Design for Usability?

- Understand user needs and goals
  - What is the user looking to do?
  - What information are they seeking?

- consistent, easy to understand, layouts
  - Use familiar navigation patterns
  - Clear headings and labels

- Optimize for different devices and screen sizes
  - Responsive design techniques
  - Test on multiple devices

---

## Techniques For Mobile Design

- **Responsive Design** - a web design approach that ensures website adapt to different screen sizes and devices.
  - **Graceful Degradation** - Design the desktop website first and modify the design to fit smaller screens.
  - **Progressive Enhancement** - A "mobile first" design methodology that begins with designing the website for the smallest device and then adapts the design for larger screens.

---

## Why Does the Industry Prefer Mobile First?

- Around 60% of global web traffic comes from mobile devices (Statista, 2023)
- Its easier to scale up a design for larger screens than to scale down a complex design for smaller screens.
  - HTML itself is responsive by default (for the most part). So if your site doesn't work on mobile, its likely due to CSS targeting desktops also applying on mobile.

---

## Building Mobile First vs Designing Mobile First

- **Building Mobile First** - Writing HTML and CSS code that prioritizes mobile devices first, then adding styles for larger screens using media queries.
- **Designing Mobile First** - Creating wireframes and mockups for mobile devices first, then adapting them for larger screens.

---

## How do I even start designing a website?

1. Define your goals and target audience
   - This will guide all your design decisions.
2. Plan your content and structure
   - sitemap
   - content inventory
3. Create wireframes and/or mockups
4. Develop the website using HTML, CSS, and JavaScript

---

## Lets design a website!

- I'm your customer.
- I'm making a web framework that allows developers to make 3D games that run in the browser.
- I want a marketing website to grow the developer ecosystem for my framework.
- I would like to announce the major version releases of my framework on this website.
- I want to have documentation for my framework on this website. I have the documentation as HTML files you can just add to the site.

---

## How do I go from wireframe to website?

- Start with a basic HTML structure and content
- Add CSS for layout and styling
- Use media queries for responsive design
  - Start with styles for mobile devices first
  - Add styles for larger screens as needed

---

## Media Queries

- **media query** - A CSS media query is a combination of media type and optionally one or more media feature expressions that evaluate to true or false.

  ```css
  /* Media Query for 1024px and above */
  @media only screen and (min-width: 1024px) {
    body {
      background-color: lightblue;
    }
  }
  ```

---

### Media Queries - Components

- **Media Type** - The type of device the styles are intended for (e.g., screen, print).
- **Media Features** - Conditions that must be met for the styles to apply (e.g., min-width, max-width, orientation).
- **Logical Operators** - Used to combine multiple media features (e.g., and, or, not).

---

## Common Breakpoints

- 320px — 480px: Mobile devices
- 481px — 768px: iPads, Tablets
- 769px — 1024px: Small screens, laptops
- 1025px — 1200px: Desktops, large screens
- 1201px and more — Extra large screens, TV
