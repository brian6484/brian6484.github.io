---
layout: post
title: Ajax button not showing up
category: Ajax
tags:
  - Ajax
---

## Issue
```javascript
$('#iarlogs-table tbody').on('click', '.iarReqMsgBtn', function(e) {
    e.preventDefault(); // Prevents the default click behavior of the button
    const data = $('#iarlogs-table').DataTable().row($(this).closest('tr')).data();
    $('#detailIarLogsModal').modal('show');
    // Perform some action with the data, such as displaying it on the modal
});

```

I had this in const clickEventIarLogsTableRow() where an ajax button is meant to pop up upon being clicked. But I could see the object being printed out in console.log() in F12 but button was not popping up. So I asked my master, Sensei GPT, and he laid out some cautions, specifically

`Make sure that the button element in your HTML has the class name iarReqMsgBtn, and that the DataTable instance has been initialized properly before attaching the event listener. Also, make sure that the modal element with the ID #detailIarLogsModal exists in your HTML and has the necessary content to display the data.
`

Make sure the modal element with id #detailIarLogsModal exists in the HTML!! That was the solution cuz when I was pasting the html code, the id was just #detailLogsModal instead of #detailIarLogsModal. 
