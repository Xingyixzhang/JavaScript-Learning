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
        })
        
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

- Additional Selector Features
