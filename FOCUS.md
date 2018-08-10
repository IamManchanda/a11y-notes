# Focus

## What is Focus?

Focus refers to the control on the computer screen that receives input from the keyboard and from the clipboard when you paste. You're probably familiar with focus for text fields. In order to type in a text field you first have to go over with your mouse and click on it. Well that act of clicking on the text field, that's actually what focuses it. You may also know that if you then press the tab key it will then move focus to the next text field or available control.

Now some users drive the computer entirely with the keyboard or some other type of discrete input device. For those users, focus is absolutely critical. It's their primary means of reaching everything on the screen. And so for that reason the Web AIM checklist states in section 2.1.1, that all page functionality should be available using the keyboard, unless it's something you couldn't normally do with a keyboard like free hand drawing or something like that. 

Learning the Focus is a great place to start learning about accessibility because obviously we all know how to use a keyboard. It's very easy to relate to and test, and it benefits virtually all of our users. There's users out there with motor impairments which could be caused by anything from paralysis or even just a broken arm. Those folks may be relying on a keyboard or switch device to navigate your page, so a good focus strategy is going to be absolutely critical for them. 

And for the power users out there, those folks who know every keyboard shortcut on their machine and hate having to use the mouse, well, for them, being able to navigate, for instance, a form on your site, is just going to make them more productive. 

So well-implemented focus strategy means everyone using your application will have a better experience. And as we'll see in the next few lessons, the work that we do today on focus is actually an important primer for supporting assistive technology users.

Focus determines where keyboard events go in the page. The currently focused item is often indicated by a focus ring, where the actual styling of that ring depends on the browser and any additional styling that the page author may have applied. As a user, you can control which element is currently focused using your keyboard.

 Pressing the Tab key will move focus forward through the document. Shift+Tab moves focus backwards. And you can use the arrow keys to move focus around within a component like for example, select component. This tab ordering (Tab for forward, ShiftTab for backward) is called, creatively enough, the tab order and making sure your application has a logical tab order is an important step for A11y. 

Now built-in interactive HTML elements like input, button, and select are all implicitly focusable. Meaning that they're automatically inserted in the tab order and that they also have built-in keyboard event handling. But not all elements are focusable and they're not implicitly inserted in the tab order and that's by design. There's generally no need to focus something if a user can't interact with it or provide it some sort of input. Use TabIndex (0 & -1) if you need to put focus on an element which are not natively focusable.

## Managing Focus for special cases

You shouldn't add tab index to site content as a general rule. But there is one exception to this and that's when you're manipulating the page, in response to a user action. 

A scenario might be that a user goes and clicks on one of these menu items and the page then does an animated scroll, down to that particular section. Or, if you are building a single page web app, clicking on one of the navigation links changes the content of the page without doing a full page refresh. In either of these situations, you'll want to pick an appropriate header, give the tab index of **-1** so it doesn't appear in the natural tab order, and call its focus method after the user has taken their action. 

This process is known as Managing Focus, and it's an extremely important technique that keeps the user's interactive context in sync with the visual representation of the site. Here's how you can implement this

```html
<h2 tabindex="-1"></h2> <!-- Default State on headers -->
```

```javascript 
focus(); // When user click on respective nav link to focus on that specic part of the page
```

## Skip Links

Skip Links are another really useful technique for improving A11y. On most websites, the main content is usually not the first thing in the DOM, instead we often begin with navigation, sublists, side bars, hamburger menus, and other bits of page scaffolding. This means that keyboard and screen reader users must first navigate through all of this content before they can get at the actual heart of the page. 

For users with motor impairments this is especially frustrating. A user who's unable to move their arms might be navigating the page with a switch device, which they activate by tapping their head. This user is going to have to tap over and over again to get through all of these elements before they can get to our content, and that's not cool. 

Thankfully, there's an easy to implement solution to this problem. Let's create a hidden link that allows keyboard and switch device users the ability to jump straight to our page content. These links are often referred to as skip links.

```html
<a href="#main-content" class="skip-link">Skip to main content</a>
<nav>
<!-- Nav content -->
</nav>
<main id="#main-content" tabindex="-1">
<!-- Main Content -->
</main>
```

```scss
.skip-link {
  position: absolute;
  top: -40px;
  left: 0;
  /* more css like background, color, spacing */
  z-index: 100; /* Choose z-index wisely. */

  &:focus {
    top: 0;
  }
}
```
