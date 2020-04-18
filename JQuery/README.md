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
#### Useful Link: [jQuery Selectors (Interactive Experiment with Selectors](http://codylindley.com/jqueryselectors/)
## Interact with the DOM
## Handle Events
## Work with AJAX Features
