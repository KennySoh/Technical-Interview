Comparing Front End Approaches
https://medium.com/actualize-network/comparing-frontend-frameworks-part-1-introduction-6cf3d49e42cf
## Jquery 

### Generating a list of div tags from list of notes. 
```
var notes=[
  {id:1, body:"This is a first test", timestamp: Date.now()},
  {id:2, body:"This is a second test", timestamp: Date.now()},
  {id:3, body:"This is a third test", timestamp: Date.now()}  
];

notes.forEach(function(note){
  $('.note-selectors').append(
    '<div class="note-selector">' +
      '<p class ="note-selector-title">' + note.body + '</p>'+
      '<p class ="note-selector-timestamp">' + note.timestamp + '</p>' +
    '</div>'
  )
});
```

### Use methods to sort and format notes
Now let's make helper methods to make sure the notes are sorted (newest first) and formated properly (titles should be computed form the body, timestamps should be converted from milliseconds into a human readable string).
```
function transformNotes(notes){
  return notes.slice().sort(function(a,b){
    return b.timestamp - a.timestamp;
  });
}

function formatTitle(body){
  var maxLength = 20;
  if(body.length >maxLength){
    return body.substring(0,maxLength -3) + '...';
  } else if (body.length ==== 0) {
    return "New note";
  } else {
  return body;
  }
}

function formatTimestamp(timestamp){
  return new Date(timestamp).toUTCString();
}
```
Inserting methods into for loop
```
transformNotes(notes).forEach(function(note){
  $('.note-selectors').append(
    '<div class="note-selector">' +
      '<p class ="note-selector-title">' + formatTitle(note.body) + '</p>'+
      '<p class ="note-selector-timestamp">' + formatTimestamp(note.timestamp) + '</p>' +
    '</div>'
  )
});
```
### Select a note on title click
Clicking on a note title should both highlight the selected note on the left as well as display the contents in the editor on the right. 

***
1. Keep track of selected note , default first element
```
var notes = [
  {id: 1, body: "This is a first test", timestamp: Date.now()},
  {id: 2, body: "This is a second test", timestamp: Date.now()},
  {id: 3, body: "This is a third test", timestamp: Date.now()}
];
var selectedNote = notes[0];
```
2. binding between the DOM and the data in JavaScript.   
Keep it in data- attribute . 
```
function domCreateNoteSelectors(notes, selectedNote) {
  transformNotes(notes).forEach(function(note) {
    var $noteSelector = $( //$ is a convention to signal dom variables
      '<div class="note-selector' + (note === selectedNote ? ' active' : '') + '">' +
        '<p class="note-selector-title">' + formatTitle(note.body) + '</p>' +
        '<p class="note-selector-timestamp">' + formatTimestamp(note.timestamp) + '</p>' +
      '</div>'
    );
    $noteSelector.data(note); // This puts the relevant dictionary into data- 
    $('.note-selectors').append($noteSelector);
  });
}
```
3. Now that we have data binding, we’ll need to make an event listener to trigger whenever the user clicks on a note title . 
- Changing the class of node
- The note data is extracted from the DOM using $(this).data(), and is passed to a separate domUpdateNoteEditor function:
```
$('.note-selectors').on('click', '.note-selector', function() {
  $('.note-selector').removeClass('active');
  $(this).addClass('active');
  domUpdateNoteEditor($(this).data());
});
```
4. Another function to Update Selected Note
```
function domUpdateNoteEditor(selectedNote) {
  $('.note-editor-info')
    .html(formatTimestamp(selectedNote.timestamp));
  $('.note-editor-input')
    .val(selectedNote.body);
}
```
***

# JQuery Data tables

https://mdbootstrap.com/docs/jquery/tables/sort/
https://datatables.net/manual/data/
```
data = [
    {
        "name":       "TEST?",
        "position":   "System Architect",
        "salary":     "$3,120",
        "start_date": "2011/04/25",
        "office":     "Edinburgh",
        "extn":       "5421"
    },
    {
        "name":       "Garrett Winters",
        "position":   "Director",
        "salary":     "$5,300",
        "start_date": "2011/07/25",
        "office":     "Edinburgh",
        "extn":       "8422"
    }
]
table.clear().draw();
table.rows.add(data); // Add new data
table.columns.adjust().draw(); // Redraw the DataTable
table.order( [[ 0, 'desc' ]] ).draw( false );
```
