# JQuery Overview
## Fundamentals:
- Single-File \-> **Cross-Browser** \-> **Selector** feature \-> Rich **Event** Infrastructure \-> Rich support for **AJAX** \-> Rich variety of **Plugins**
- **$(document).ready()**: detect when a page has loaded and is ready to use. It is called once **DOM Hierarchy** is loaded, 
but **BEFORE** all images have loaded.
```javascript
<script type="text/javascript">
    $(document).ready(function(){   // Inline Anonymous function
        // Perform Actions here
    });
</script>
```
