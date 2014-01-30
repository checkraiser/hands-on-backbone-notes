Backbone.js Routers
--

The Rails way
--

- Remove the 'Hello From Backbone' alert from our ScratchPad initialize method in
  app/assets/javascripts/scratch\_pad.js.coffee
- Create a Rails controller `NotesController`

        class NotesController < ApplicationController
          helper_method :notes, :note

          def notes
            @_notes ||= Note.all
          end

          def note
            @_note ||= notes.find(params[:id])
          end
        end

- Create an index view for the Note model `index.html.erb`

        <ul>
          <% @notes.each do |note| %>
            <li>
              <dl>
                <dt>Title</dt>
                <dd><%= link_to note.title, note %></dd>
                <dt>Content</dt>
                <dd><%= note.content %></dd>
              </dl>
            </li>
          <% end %>
        </ul>

- Create a show index view for the Note model

        <h1><%= note.title %></h1>
        <p><%= note.content %></p>

- Generate a Note Rails model with title and content
  - User the seed file to create three new Notes

        Note.destroy_all

        Note.create(title: 'The first note', content: 'I am a note!')
        Note.create(title: 'The second note', content: '')
        Note.create(title: 'The third note', content: 'more notes')

- Add Note resources line to the config/routes.rb file
- Commit!

Backbone Router
--

- Create a router for our Scratch Pad app at `app/assets/javascripts/router/scratch_pad_router.js.coffee`
- Define a routes hash in the new router
  - Notice that either a method name or a function can be passed to a Backbone
    route
- Define an index route that points to a method that calls the `alert` method
  and prints a message saying "You requested the index page"
- Define a Note show route that points to a `showNote` method that calls the `alert` method and displays a message that tells the user they're in the show view and repeats the id in the url

        class App.Routers.ScratchPadRouter extends Backbone.Router
          routes:
            '': -> alert("You requested the index page")
            '/notes/:id': 'showNote'

          showNote: (id) ->
            alert("You requested the note with the id of #{id}")

- Return to the `scratch_pad` Javascript file and update the initialize method
  - Instantiate our new router
  - Add a call to the Backbone.history.start method

        initialize: ->
          new @Routers.ScratchPadRouter
          Backbone.history.start()

- Now return to the browser and navigate to notes/1 notice it doesn't work
- Now navigate the browser to #note/1
- Pass pushState: true to the Backbone.history.start method call to remove the
  need for the hash in the url

        initialize: ->
          new @Routers.ScratchPadRouter
          Backbone.history.start(pushState: true)


- Commit!
