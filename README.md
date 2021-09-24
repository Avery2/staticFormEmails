# staticFormEmails

How to put forms that send emails on action into static sites without redirect

## Step 1

Make a simple HTML form.

```html
<form>
  First name:<br>
  <input type="text" name="firstname"><br>
  Last name:<br>
  <input type="text" name="lastname">
  <input type="submit" value="Submit">
</form>
```

## Step 2

Make a google form with the same fields.

![alt text](https://github.com/toperkin/staticFormEmails/raw/master/newForm.png)

## Step 3

We need to know what google calls these fields. Make a pre-filled form, fill it with anything, and grab the link.

![alt text](https://github.com/toperkin/staticFormEmails/raw/master/prefilled.png)

![alt text](https://github.com/toperkin/staticFormEmails/raw/master/getlink.png)

```
https://docs.google.com/forms/d/14lh6MIQOy9j3jWzEl7BysxEe4p9OoU9WN3tytbQjj1I/viewform?entry.810989529=garbageFirstName&entry.463380756=garbageLastName
```

## Step 4

Use the entry fields from the pre-filled link for your form name/ids, and set the action to direct to your google form. Also, add some hidden\_iframes, this is used to block the redirect. Don't forget to change the final link from `viewform?` to `formResponse?`.

```html
<form name="gform" id="gform" enctype="text/plain" action="https://docs.google.com/forms/d/14lh6MIQOy9j3jWzEl7BysxEe4p9OoU9WN3tytbQjj1I/formResponse?" target="hidden_iframe" onsubmit="submitted=true;">
  First name:<br>
  <input type="text" name="entry.810989529" id="entry.810989529"><br>
  Last name:<br>
  <input type="text" name="entry.463380756" id="entry.463380756">
  <input type="submit" value="Submit">
</form>

<iframe name="hidden_iframe" id="hidden_iframe" style="display:none;" onload="if(submitted) {}"></iframe>
```

## Step 5

Add some javascript to keep track of what happens after a submit.

```html
<script src="assets/js/jquery.min.js"></script>
<script type="text/javascript">var submitted=false;</script>
<script type="text/javascript">
$('#gform').on('submit', function(e) {
  $('#gform *').fadeOut(2000);
  $('#gform').prepend('Your submission has been processed...');
  });
</script>
```

That's it. You now have an HTML form that upon submits completes the google form (which can easily be set up to populate a spreadsheet and/or email you), but DOES NOT REDIRECT, instead just fades away and is replaces with a friendly message.

## Demo

Here are some demo shots from a website I'm making:

Here's just an empty form with some CSS styling...

![alt text](https://github.com/toperkin/staticFormEmails/raw/master/1.png)

You fill it out with whatever ...

![alt text](https://github.com/toperkin/staticFormEmails/raw/master/2.png)

The user sees just this upon submit...

![alt text](https://github.com/toperkin/staticFormEmails/raw/master/3.png)

This is what it looks like in my response spreadsheet...

![alt text](https://github.com/toperkin/staticFormEmails/raw/master/4.png)
