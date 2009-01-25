---
layout: post
title: Character Counter
---

<div style="text-align:center">
  <textarea id="text" rows="10" cols="60">Type stuff here.</textarea>
  
  <h2>
    about
    <span id="words">0</span> words,
    <span id="chars">0</span> characters.
  </h2>
</div>

<script type="text/javascript">
  function updateCounts() {
    var text = $("#text")
    var chars = $("#chars")
    var words = $("#words")

    words.html(text.val().split(/\s+/).length)
    chars.html(text.val().length)
  }

  $(document).ready(function() {
    $("#text").keyup(updateCounts)
    updateCounts()
    $("#text").focus().select()
  })
</script>
