# JQuery Overview
## Introduction:
- Single-File \-> **Cross-Browser** \-> **Selector** feature \-> Rich **Event** Infrastructure \-> Rich support for **AJAX** \-> Rich variety of **Plugins**
- **$(document).ready()**: detect when a page has loaded and is ready to use. It is called once **DOM Hierarchy** is loaded, 
but **BEFORE** all images have loaded.
```javascript
<script type="text/javascript">
    // Window.onload:
    Window.onload = function() {
        alert('Window loaded');
    };
    // jQuery.ready: -- display before window.onload.
    $(document).ready(function(){   // Inline Anonymous function
        // Perform Actions here
        aleart('DOM loaded');
    });
</script>
```
- Useful documentation: [ JQuery API Documentation ](https://api.jquery.com/html/)
## Using jQuery Selectors
- What are **Selectors**: way to select node(element) from the DOM.
- Selector **Syntax**: **$(selectorExpression)**/ **jQuery(selectorExpression)**
- Select nodes by **Tag Name**/ **ID**/ **Class Name**/ **Attribute Value**
#### Tag Name: 
1. **$('p')**: selects all \<p> elements; **$('a')**: selects all \<a> elements.
2. **$('p, a, span')**: selects all paragraphs, \<a>, and \<span> elements.
3. **$('ancestor descendant')**: ex. **$('table tr')** selects all tr elements that are descendant of the table element.
```javascript
<script type="text/javascript">
    $(document).ready(function(){
        $('div').css("background-color", 'Green');
        
        $('div').each(function() {
            alert($(this).html());
        });
        
        var coll = $('div, span');
        alert(coll.length);
        
        $('div, span').css('propName', 'value');
    });
</script>
```
#### ID/Class Selector:
- **$('#myID')**: selects \<p id="myID"> element
- **$('.myClass')**: selects \<p class="myClass"> element
- **$('.BlueDiv, .RedDiv')**: selects all elements containing class BlueDiv and RedDiv
```javascript
<script type="text/javascript">
    $(document).ready(function(){
        $('.BlueDiv, div.RedDiv').css('border', '2px solid red');
    });
</script>
```
#### You may combine element names:
- ex. **$('a.myClass')**: selects only \<a> tags with class="myClass"
#### Attribute Value: *When see [], think the word "where"*
1. **$('a[title]')**: selects all \<a> elements that have a title attribute.
2. **$('a[title="Programming Info"]')**: selects all \<a> elements that have a "Programming Info" title attribute value.
```javascript
<script type="text/javascript">
    $(document).ready(function(){
        alert($('div[title]').length);
        
        var divs = $('div[title="Div Title"]');     // title name "..." is CASE-Sensitive!
        alert(divs.length);
        
        var inputs = $('input[type="text"]');
        inputs.css('background-color', 'yellow');
    });
</script>
```
#### Select Input Nodes
1. **$(':input')**: selects all input elements
2. **$(':input[type="radio"]')**: targets all radio buttons on the page.. not most efficient selector for that though, since it will find all input types then filter through to find all radio button types.
```javascript
<script type="text/javascript">
    $(document).ready(function(){
        var inputs = $(':input');
        alert($(inputs[1]).val());
        
        $('form :input').each(function() {  // could be more efficient than $(':input').
            var elem = $(this); // Wrapped in a jQuery wrapper.
            alert(elem.val());
            // alert(elem.val('Foo'));  // set the value of all input to "Foo".
        });
    });
</script>
```
#### Additional Selector Features
- using **contains** in Selectors
**:contains()**: selects elements that match the contents within the contains exception.
```javascript
$('div:contains("pluralsight")')    // divs that contains the text pluralsight, the match is CASE-Sensitive!!
<div>Expert pluralsight Training</div>  // Example.
```
- select **even/ odd rows** in a table \--> NOTE: the index is **0 based**.
**$('tr:odd')** (1,3,5,7...) and **$('tr:even')** (0,2,4,6...)
```javascript
<script type="text/javascript">
    $(document).ready(function () {
        $('tr:odd').css('background', 'green');
        $('tr:even').css('background', 'yellow');
        $('tr:first-child').css('background', 'red');   // highlight the first row of tables.
        $('#DataTable tr:first-child').css('background', 'green'); // Specify the table.
        $('.tableID tr:odd').css('background', 'green');
    });
</script>
```
- select the **First Child**
**$('*element*:first-child)**: selects the first child of every element group.
```javascript
$('span:first-child')

<div>
    <span>First Child, First Group</span>
    <span>Second Child, First Group</span>
</div>
<div>
    <span>First Child, Second Group</span>
    <span>Second Child, Second Group</span>
</div>
```
- using **Starts/Ends With//Contains** in selectors
**[*attribute* ^= "*value*"]**: select all elements with an attribute that **begins** with stated value.
**[*attribute* $= "*value*"]**: select all elements with an attribute that **ends** with stated value.
**[*attribute* *= "*value*"]**: select all elements with an attribute that **contains** the stated value.
```javascript
$('input[value^="Events"]')     // selects any input element whose value attribute begins with "Events"

<input type="button" value="Events-World" />
<input type="button" value="Events-National" />
<input type="button" value="Events-Local" />

$('input[value$="Events"]')     // selects any input element whose value attribute ends with "Events"

<input type="button" value="World Events" />
<input type="button" value="National Events" />
<input type="button" value="Local Events" />

$('input[value*="Events"]')     // selects any input element whose value attribute contains "Events"

<input type="button" value="World Events 2020" />
<input type="button" value="National Events 2020" />
<input type="button" value="Local Events 2020" />
```
#### Useful Link: [jQuery Selectors (Interactive Experiment with Selectors)](http://codylindley.com/jqueryselectors/)
## Interact with the DOM
#### Iterate through nodes 
```javascript
$('div').each(function(index){
    alert(index + '=' + $(this).text());
});
// You can also do the following but the above is better.
$('div').each(function(index, elem){
    alert(index + '=' + $(elem).text());    // elem == this.
});

// var output = $('#OutputDiv');
var html = "";
$('div.BlueDiv, div.RedDiv').each(function (index){
    // $('#OutputDiv');     better practice to have output variable first since each time called will look at whole doc to find the id tag.
    // output.html(output.html() + "<br />" + index + " " + $(this).text());
    html += "<br />" + index + " " + $(this).text();
});
var output = $('#OutputDiv');
output.html(html);
```
#### Modify DOM Object Properties and Attributes
```javascript
// this: raw DOM object without jQuery wrapper for the access of jQuery APIs.
$('div').each(function(i) {
    this.title = "My index = " + i; // title is the DOM object Property.
});


// .attr(): access object attributes
var val = $('#CustomerDiv').attr('title');  // Retrieves the value of the title attribute.


// .attr(attributeName, valueToSet): Access the object's attribute and modify the value.
$('img').attr('title', 'My Image Title');


// Modify multi attributes, by passing a JSON object containing name/value pairs:
$('img').attr({                         // { ..:..., ..:..., ..:... } JSON anonymous object
    title: 'My Image Title',
    style: 'border: 2px solid black;'
});


// Chaining, instead of seperately calling which iterate through objects multi times:
$('div.BlueDiv, div.RedDiv')
    .attr(
        { 
            title: 'My Image Title',
            style: 'border: 2px solid black;'   // jQuery: css ~ JSON: style.
        }
    )
    .css('background-color', 'yellow')
    .css('color', 'black')
    .css('font-size', '20px')
```
#### Add/Remove Nodes
- Key methods handling **Inserting** nodes into elements: (*Saves time since no need to do through the doc*)
1. **.append()**
2. **.appendTo()**
```javascript
// Append: adds children at the END of the matching element.

// To add (office) into each .officePhone class element:
$('<span>(office)</span>').appendTo('.officePhone');
// =========================== OR =========================
$('.officePhone').append('<span>(office)</span>');
```
3. **.prepend()**
4. **prependTo()**
```javascript
// Prepend: adds children at the BEGINNING of the matching element.

// To add (office) into each .officePhone class element:
$('<span>(office)</span>').prependTo('.officePhone');
// =========================== OR =========================
$('.officePhone').prepend('<span>(office)</span>');
```
- Wrapping elements: **.wrap()**
```javascript
<div class="state">Arizona</div>

$('.state').wrap('<div class="US_State" />');

// RESULT:
<div class="US_State">
    <div class="state">Arizona</div>
</div>
```
- To remove nodes from the DOM: **.remove()**
```$('.phone, .location').remove();```: remove Objects with .phone/.location classes from the DOM.
#### Modify Styles and Classes
```javascript
// Chaining 3 functions, Change the Styles:
$('div.BlueDiv, div.RedDiv')
    .attr(
        { 
            title: 'My Image Title',
            style: 'border: 2px solid black;'   // jQuery: css ~ JSON: style.
        }
    )
    .css({
        'background-color': 'yellow',
        'color': 'black',
        'font-size': '20px'
    }).text('Changed Color');
    
/* Key methods for working with CSS class attributes: 
 *      .addClass() -- add >=1 class names to the class attribute of each matching element.
 *      .hasClass()
 *      .removeClass() -- remove >=1 classes.
 *      .toggleClass() -- if exist, remove it; if not exist, add it.
 */
 
 $('p').addClass('classOne');
 $('p').addClass('classOne classTwo');
 
 if ($('p').hasClass('styleSpecific');){
    // Perform work.
 }
 
 $('p').removeClass();  // remove all classes.
 $('p').removeClass('classOne');
 $('p').removeClass('classOne classTwo');
 
 <style type="text/css">
    .highlight { background: yellow; }
 </style>
 $('#PhoneDetails').toggleClass('highlight');
 
 // in <script>:
 function FocusBlur(textBox) {
    $(textBox).toggleClass('highlight');
 }
 // in html <input>:
 <input id="FirstTextBox" onfocus="FocusBlur(this)" onblur="FocusBlur(this)" type="text" />
 <input id="SecondTextBox" onfocus="FocusBlur(this)" onblur="FocusBlur(this)" type="text" />
```
## Handle Events
- [jQuery Event Doc](https://api.jquery.com/category/events/)
```javascript
<script type="text/javascript">

    // Handle event the old-fashion way using javascript:
    var button = document.getElementById('SubmitButton');
    if (document.addEventListener){ // Most browser syntax:
        button.addEventListener('click', function() { alert('Clicked Button'); }, false);
    }
    else{   // Internet Explorer handles it differently:
        button.attachEvent('onclick', function() { alert('Clicked IE Button'); });
    }
    
    // .click(handler(eventObject))
    $('#myID').click(function() {
        alert('The element myID was clicked');
        
        // Raise a click event:
        $('#otherID').click(function() {
            $('#myID').click(); 
        });
    });
</script>
```
1. Click Event
```javascript
<script type="text/javascript">
    $(document).ready(function () {
        WireEvents();
        // More functions...
    });
    
    function WireEvents() {
        $('#SubmitButton').click(function () {
            alert('Button Clicked.');
            
            var fnval = $('#FirstNameTextBox').val();
            var lnval = $('#LastNameTextBox').val();
            $('#DivOutput').text(fnval + ' ' + lnval);
        });
        
        // 2. Change Event. Handle Select.
        
        // 3. Mouse Events.
    }
</script>
```
2. Change Event
```javascript
$('#StateSelect').change(function() {
    alert($(this).val());
});

// ======================= OR ===================
// Note that the myInputs class can be attached to div, select, textarea, text...

$('.myInputs').change(function() {
    alert($(this).val());
    $(this).addClass('highlight');
});
```
3. Mouse Events
```javascript
$('#myDiv, tr').mouseenter(function () {
    Toggle($(this));    // Toggle(this);
    $(this).css('cursor', 'pointer');
})
.mouseleave(function () {
    // $(this).toggleClass('highlight');
    Toggle(this);
})
.mouseup(function (e) {
    alert($(e.target).attr('id'));
    $(this).text('X: ' + e.pageX + ' Y: ' + e.pageY);
});

function Toggle(div){
    $(div).toggleClass('highlight');
}
```
4. Binding to Events
- **.on(eventType, handler(event object))**: attaches a handler to an event for the selected element(s).
- **.off(event)**: remove a handler previously bounded to an element.
```javascript
$('#MyDiv').on('click', function () {
    // Handle the event here...
});

// .on() allows multi events to be bound to >=1 elements:
$('#MyDiv').on('mouseenter mouseleave mouseup', function () {
    $(this).toggleClass('highlight');
    $(this).css('cursor', 'pointer');
    
    // For only mouseup:
    if (e.type == 'mouseup'){
        $(this).text('X: ' + e.pageX + ' Y: ' + e.pageY);
    }
});

// to unbound $('#test').click(handler); : 
$('#test').off();

// To specify targeted event:
$('#test').off('click');
```
- Useful website: [jQuery Source Viewer](https://j11y.io/jquery/)
5. **live()**, **delegate()**, and **on()**
- **delegate()** is a newer version of **live()** added in jQuery 1.4, works even when new objects are added into the DOM.
- **undelegate()**: to stop delegate event handling.
```javascript
$('#Divs').delegate('.someClass', 'click', func() {
    // any child of #Divs that's .someClass will bubble up to #Divs (NOT all the way up to DOM) ... when clicked.
});
```
- The **on()** function is a new replacement for: **bind(), delegate(), live()**, works when new objs are added into the DOM.
```javascript
// instead of $('tr').on('click'..., use the parent and let the event bubble up. more efficient.

$("#MyTable tr") tbody").on("click", "tr", function(event) {
    alert('Row was clicked and bubbled up');
});

// Read: find the obj with MyTable id, in its tbody, on the click of tr, invoke the function...
```
- Using **on()** with a *map*:
```javascript
$("#MyTable tr").on({
    mouseenter: function() {
        $(this).addClass("over");
    },
    mouseleave: function() {
        $(this).addClass("out");
    }
});
```
6. Hover Events
- **$(selector).hover(handlerIn, handlerOut)**
- **handlerIn** = *mouseenter*; **handlerOut** = *mouseleave*.
```javascript
$('#target').hover(
// mouseenter highlights the target :
    function(){
        $(this).css('background-color', '#00FF99');
    },
// mouseleave set it back to white :
    function(){
        $(this).css('background-color', '#FFFFFF');
    }
);

// Another option: $(selector).hover(handlerInOut):
$('p').hover(function() {
    $(this).toggleClass('over');
});
```
## Work with AJAX Features
- AJAX is a way to update parts of the page without reloading the whole page.
#### jQuery AJAX Functions
- jQuery allows Ajax requests to be made from a page:
1. Allow parts of a page to be updated
2. Cross-Browser Support
3. Simple API
4. Get & POST supported
5. Load JSON, XML, HTML or even scripts
#### Loading HTML Content from the server
#### Make GET/ POST Requests
#### Intro to the ajax() function
