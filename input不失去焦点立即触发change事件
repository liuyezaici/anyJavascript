##链接
<http://forum.jquery.com/topic/how-to-fire-change-event-immediately-for-input-element-without-losing-focus>

$('input').keyup(function(){
      $(this).change();
})

or like this ?:

$(#'myInput').val('someNewVal created in app code').change();

If it's first case it seems easier to add other events to your change handler

$('input').on('keyup change', function(){
      $.doSomething()
})