# JavaScript - Scroll by dragging
[Try out](https://jsfiddle.net/hmxn4evk/6/)

```html
<!-- The drag-container must be scrollable in order for this to work -->
<div id="drag-container">
    <div class="clickable-element"></div>
    <!-- Many more clickable-elements so that they are overflowing -->
</div>
<script>
  let wasDragging = false;
  let previousMouseEvent = undefined;

  const dragContainer = document.getElementById('drag-container');

  // First we have to register a click event on the capture-phase that captures the click that would have been fired on an 
  //  clickable-element in the case the user started and ended the drag on the same element
  dragContainer.addEventListener(
    'click',
    captureClickIfWasDragging,
    true // THIS IS IMPORTANT (Registers event on capture instead of bubbling phase)
  );

  function captureClickIfWasDragging(e) {
    if (wasDragging) {
      e.preventDefault();
      e.stopPropagation();
    }
  }


  dragContainer.addEventListener('mousedown', startDrag);

  function startDrag(e) {
    wasDragging = false;

    previousMouseEvent = e;

    // Prevent ghost-dragging of clickable-elements
    e.preventDefault();
    
    dragContainer.addEventListener('mousemove', drag);
    dragContainer.addEventListener('mouseup', endDrag);
    dragContainer.addEventListener('mouseleave', endDrag);
  }

  function drag(e){
      dragContainer.scrollTop -= e.screenY - previousMouseEvent.screenY;
      dragContainer.scrollLeft -= e.screenX - previousMouseEvent.screenX;
      
      wasDragging = true;
      previousMouseEvent = e;
  }

  function endDrag() {
      dragContainer.removeEventListener('mousemove', drag);
      dragContainer.removeEventListener('mouseup', endDrag);
      dragContainer.removeEventListener('mouseleave', endDrag);
  }
</script>
```
