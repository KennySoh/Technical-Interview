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
```

```
