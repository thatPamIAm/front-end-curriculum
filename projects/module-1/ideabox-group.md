---
title: IdeaBox Group
---

## Overview

Every developer has more ideas than time. As David Allen likes to say "the human brain is for creating ideas, not remembering them." In this project, we'll be building an application a new client that records and archives our ideas (good and bad alike).

Throughout the project, one of our focuses will be on providing a fluid and responsive client-side interface. To this end, we'll rely on JavaScript and to implement snappy filtering in the browser, and `localStorage` to persist our wonderful ideas between sessions.  Our goal is to also incorporate an agile workflow by incorporating two weekly sprints.

*Note*: Expectations listed for Iteration 0-1 should be complete by your first check-in. No JavaScript should be written before that check-in, unless you get approval to move ahead with functionality from your Project Manager.

## Learning Goals

* Continue to improve on building responsive client-side applications with good user feedback
* Understand how to implement client-side data persistence using `localStorage`
* Understand what it looks like to have a separate data model (using a class) and DOM model
* Utilize `data-*` attributes
* Incorporate & iterate over arrays in order to filter what is being displayed
* Craft code with clean style, using small functions that show trends toward DRYness and SRP

## Setup

- Complete a DTR
- Create a slack channel for all team members and your Project Manager.
- Create a directory called `ideabox`, with `index.html` and `styles.css` files inside of it. Initialize and create a GitHub project. Add all team members and your Project Manager as collaborators.
- Deploy your application to GitHub Pages.
- In the team channel, drop the repo link and GitHub pages link.

## Progression

### Iteration 0 - Desktop Layout

Plan then write the HTML and CSS so that you application matches this comp. Based on what you are building, you can anticipate that the Idea "cards" will not always be there on page load, but for now, they should.

Use the same text on your cards that is used in the spec so you can ensure your spacing/sizing is accurate.

![desktop specs][desktop-base]

<img class="medium" src="./assets/ideabox-group/colors.png">

You will need the `svg` files for the star, delete, and menu icons. [Here's the link to download the `svg` icons.](https://drive.google.com/drive/folders/18xpWplI0tpXIK1omBZeq04LEx2OMzzMK?usp=sharing)

[desktop-base]: /assets/images/projects/ideabox/ideabox-redux-01.jpg

### Iteration 1 - Mobile Layout

Now that your Desktop Layout is in place, it's time to write some media queries so this is a responsive site.

Full mobile layout:

![full mobile layout][mobile-full]

Full mobile layout with open navigation:

![full mobile layout with navigation][mobile-full-navigation]

[mobile-full]: /assets/images/projects/ideabox/ideabox-redux-02.jpg
[mobile-full-navigation]: /assets/images/projects/ideabox/ideabox-redux-03.jpg

### Iteration 2 and beyond

After you have completed Iterations 0-1, your Project Manager will provide you with the next iteration.

<!-- Everything below will be commented out, only for Instructors to see -->

### Architecture

For this project, we'll be increasingly thinking about the "data model" and "DOM model" as separate entities. We'll be using:

- JSON and `localStorage` to persist data on page reload.
- vanilla JavaScript to manage client-side interactions.

Your entire application will consist of one HTML page or template. You will have two JavaScript files, for now:

1. An `idea.js` file that contains an `Idea` class.
  * `Idea` methods must include, but are not limited to:
    1. `constructor`
    2. `saveToStorage` (should only have one job which is to save the instance to storage)
    3. `deleteFromStorage`
    4. `updateIdea` (should be able to update the idea's title, body, or starred state)
2. A `main.js` file that contains all syndrome related JavaScript.

**Note** The `idea.js` file  must be the first script in your HTML so that your `main.js` file has access to your `Idea` class.

### Data Model

* An idea has an _id_, _title_, _body_, and _star_.
  * The _id_ should be a unique identifier. (Note: generating a random number does _not_ guarantee it will be unique)
  * _title_ and _body_ are strings.
  * _star_ is a boolean.

Each idea should be created as an object instance of the `Idea` class. Once an idea object is created, all that data can be used to update the DOM. That object should also be added to a `list` of all the ideas your application currently has. This should probably be a global variable in your `main.js`.

### Iteration 2 - Adding Ideas

As a user,
- When I click "Save",
- If I entered information in both the "Title" and "Body" input fields,
- I should see a new idea card with the provided title and body appear in the idea list

As a user,
- When I click "Save",
- If I entered information in both the "Title" and "Body" input fields,
- I should see the "Title" and "Body" input fields clear out

As a user,
- When I look at the "Save" button,
- When either the "Title" or "Body" inputs are empty,
- I should notice that the "Save" button is disabled because it is a lighter color and the cursor is not a pointer when I hover over it

As a user,
- When I click "Save",
- And a new card is successfully created,
- I should _not_ see the page reload

### Iteration 3 - Favoriting & Deleting Ideas

As a user,
- When I click the "Delete" button on an idea card,
- The card should be permanently removed from my view

As a user,
- When I click the "Star" button on an idea card,
- When the button was an outline of a star (not favorited),
- The button should now be a filled in star (favorited)

As a user,
- When I click the "Star" button on an idea card,
- When the button was a filled in star (favorited),
- The button should now be an outline of a star (not favorited)

As a user,
- When I delete or favorite any card,
- I should _not_ see the page reload

### Iteration 4 - Local Storage

As a user,
- When I create one idea successfully, then refresh the page,
- The idea card is still in the idea list

As a user,
- When I create two cards successfully, delete one, then refresh the page,
- One idea card is still in the idea list (the one I did not delete)

As a user,
- When I favorite an idea card, then refresh the page,
- That idea card is still in the "favorite" state with the filled in star icon

### Iteration 5 - Commenting on Ideas

### Architecture

In addition to your `idea.js` and `main.js`, you now need to have a `comment.js` file.

This file should hold a class, `Comment`. `Comment` methods must include, but are not limited to:
1. `constructor`
2. `saveToStorage` (should only have one job which is to save the instance to storage)
3. `deleteFromStorage`

### Data Model

* An idea now also has a _comments_ property
  * The _id_ should be a unique identifier. (Note: generating a random number does _not_ guarantee it will be unique)
  * _title_ and _body_ are strings.
  * _star_ is a boolean.
  * _comments_ is an array.

* A comment should have _content_ - a string that holds the content of a comment. If you end up completing an extension, you may need your comment class to have additional properties.


As a user,
- When I click the "Add" icon on an idea card,
- A form to add a comment appears

As a user,
- When I open the comment form on a card, type something in, and click "Add Comment",
- The text typed in is now a comment attached to this card

As a user,
- When I open the comment form on a card, type something in, and click "Add Comment",
- The "Comment" input field clears out and is ready to accept another comment

As a user,
- When I open the comment form on am idea card,
- When the "Comment" input field is empty,
- I should notice that the "Add Comment" button is disabled because it is a lighter color and the cursor is not a pointer when I hover over it

As a user,
- When I comment on an idea card, then refresh the page,
- That comment is still on the idea card
