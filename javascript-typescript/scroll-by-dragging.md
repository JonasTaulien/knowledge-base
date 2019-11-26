# JavScript - Scroll by dragging
[Try out](https://jsfiddle.net/5mkvxb3t/4/)

```html
<!-- The drag-container must be scrollable in order for this to work -->
<div id="drag-container">
    <div class="clickable-element"></div>
    <!-- Many more clickable-elements so that they are overflowing -->
</div>
<script>
    let wasDragging = false;
    let dragActive = true;

    const dragContainer = document.getElementById('drag-container');

    // First we have to register a click event on the capture-phase that captures the click that would have been fired on an 
    //  clickable-element in the case the user started and ended the drag on the same element
    dragContainer.addEventListener(
        'click', 
        (e) => {
            if (wasDragging) {
                e.preventDefault();
                e.stopPropagation();
            }
        }, 
        true // THIS IS IMPORTANT (Registers event on capture instead of bubbling phase)
    );
    
    // We start the drag on mouse down and reset the wasDragging flag
    dragContainer.addEventListener(
        'mousedown',
        (e) => {
            dragActive = true;
            wasDragging = false;
                    
            // Prevent ghost-dragging of clickable-elements
            e.preventDefault();
        }
    );

    // If the mouse moves and the drag is active, scroll the drag container and set wasDragging flag to true
    dragContainer.addEventListener(
        'mousemove',
        (e) => {
            if(dragActive){
                dragContainer.scrollTop -= e.movementY;
                dragContainer.scrollLeft -= e.movementX;
                
                wasDragging = true;
            }
        }
    );

    // In mouse up or if the mouse leaves we simple reset the dragActive flag
    dragContainer.addEventListener(
        'mouseup',
        endDrag
    );
    dragContainer.addEventListener(
        'mouseleave',
        endDrag
    );

    function endDrag(){
        if(dragActive){
            dragActive = false;
        }
    }
</script>
```