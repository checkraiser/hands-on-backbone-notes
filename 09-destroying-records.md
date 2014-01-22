Destroying Records
==

- In the show.jst.eco file add a destroy button to the note div
- ```
  <header class="title-container">
    <input type="text" class="note-title" placeholder="Title..." value="<%= @note.get('title') %>" />
  </header>
  <div class="body">
    <textarea class="note-content" placeholder="Content..."><%= @note.get('content') %></textarea>
  </div>
  <button class="destroy-note" tabindex="-1">Remove</button>
  ```
- Open the note.css.scss file
  - Add a definition for the `destroy-note` class under body
  - When hovering over the `note` dislpay the destroy-note div block
  - ```
    &:hover {
      .destroy-note {
        display: block;
      }
    }

    .destroy-note {
      postition: absolute;
      top: 7px;
      right: 5px;
      display: none;
    }
    ```
- In the show.jst.eco file set the tabindex of the `destroy-note` button to -1
- Open the ShowNote Backbone view
  - Add a client event to the destroy-note class that is handled by a
    `destroyNote` method
  - ```
    events:
      'change': 'save'
      'keydown .note-title': 'blurIfEnter'
      'focus .note-title, .note-content': 'beginEditing'
      'blur .note-title, .note-content': 'endEditing'
      'click .destroy-note': 'destroyNote'
    ```
  - Create the `destroyNote` method
    - In the method call `@model.destroy()`
    - Then call @remove to remove the view and avoid memory leaks
    - return false
  - ```
    destroyNote: ->
      @model.destroy()
      @remove()
      false
    ```

- Commit!
