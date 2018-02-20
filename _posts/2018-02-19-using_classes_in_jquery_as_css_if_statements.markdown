---
layout: post
title:      "Using HTML Classes in jQuery as CSS If Statements"
date:       2018-02-19 18:55:53 -0500
permalink:  using_classes_in_jquery_as_css_if_statements
---


While CSS can be the difference between a stale looking, bare-bones program and a vibrant, exciting webpage, it still has some rather archaic restrictions relative to other programming languages. In the case of adding a jQuery front-end to my Gift Organizer Rails app, there was nothing more restricting than a lack of If Statements in CSS.

There are multiple ways to get around this, but after lots of trail and error, I found what I felt to be the best way: switching classes through jQuery.

After a user creates a gift, it gets a button next to it that the user clicks after they have sent a thank you note to that specific gift's givers. It starts with a red background with red text "NOT THANKED". When hovered over, the text should change to "THANK?", with a black background and white text. Then, when clicked, it should change to the text "THANKED", with a green background and black text.

I initially wrote this code by changing each individual CSS property in each individual jQuery event. This got the job done but did not adhere to DRY principles by any stretch of the imagination. Ex:

```
<!--thank hover-->
<script>
  $(document).on({
      mouseenter: function () {
        $(this).css("background-color", "black");
        $(this).css("color", "white")
        if ($(this).html() === "NOT THANKED") {
          $(this).html("THANK?")
        } else {
          $(this).html("UNTHANK?")
        }
      },
      mouseleave: function () {
        if ($(this).html() === "THANK?") {
          $(this).css("background-color", "#ff4d4d");
          $(this).css("font-weight", "bold")
          $(this).css("color", "black")
          $(this).html("NOT THANKED")
        } else if ($(this).html() === "NOT THANKED") {
          $(this).css("background-color", "#ff4d4d");
          $(this).css("font-weight", "bold")
          $(this).css("color", "black")
          $(this).html("NOT THANKED")
        } else {
          $(this).css("background-color", "#3FFE7C");
          $(this).css("font-weight", "bold")
          $(this).css("color", "black")
          $(this).html("THANKED")
        }
      }
  }, '.thanked_div');
</script>
```

This is insanity. I had to write a version of this code close to 10 times. NOT THANKED CSS, THANKED CSS, NOT THANKED HOVER CSS, THANKED HOVER CSS, just to name a few. I needed to clean up. HTML classes to the rescue!

I realized I really only had three CSS scenarios, THANKED, NOT THANKED, and HOVER. So I created these as classes, each with individual CSS properties:

```
.thanked_div {
  border: 0;
  background-color: #3FFE7C;
  box-shadow: none;
  border-radius: 0px;
  font-weight: bold;
  border-style: solid;
  border-width: 1px;
  border-color: black;
  width: 97px;
}

.not_thanked_div {
  border: 0;
  background-color: #ff4d4d;
  box-shadow: none;
  border-radius: 0px;
  font-weight: bold;
  border-style: solid;
  border-width: 1px;
  border-color: black;
  width: 97px;
}

.thank_hover {
  border: 0;
  background-color: black;
  color: white;
  box-shadow: none;
  border-radius: 0px;
  font-weight: bold;
  border-style: solid;
  border-width: 1px;
  border-color: black;
  width: 97px;
}
```

Now all that is needed in each jQuery event is to change the class and the HTML.

```
<!--thank hover in-->
<script>
  $(document).on({
    mouseenter: function () {
      $(this).html("UNTHANK?")
      $(this).attr("class", "thank_hover");
    },
  }, '.thanked_div');
</script>

<!--not thanked hover in-->
<script>
  $(document).on({
    mouseenter: function () {
      $(this).html("THANK?")
      $(this).attr("class", "thank_hover");
    },
  }, '.not_thanked_div');
</script>

<!--hover out-->
<script>
  $(document).on({
    mouseleave: function () {
      if ($(this).html() === "THANK?") {
        $(this).attr("class", "not_thanked_div");
        $(this).html("NOT THANKED")
      } else if ($(this).html() === "UNTHANK?") {
        $(this).attr("class", "thanked_div");
        $(this).html("THANKED")
      }
    }
  }, '.thank_hover');
</script>
```

DRY as a bone!!
