#Using Helpers for Select, Date and Time in Rails #

###Selects and Options

We all love to use select and option tags to create dropdown menus in our forms. The HTML generally looks like this, as a refresher:

```
<select name="select">
  <option value="value1">Value 1</option> 
  <option value="value2" selected>Value 2</option>
  <option value="value3">Value 3</option>
</select>

```

This is easily done in rails, using helpers. They are convenientally known as 'select_tag' and 'option value'.

We can create a simple select by passing a symbol to 
`select_tag` to indicate the name of the value being passed. Example:

```
<%= select_tag(:age, '<option value="1">old</option>, <option value="2"> young</option>) %>
```

It is much easier to use an `options_for_select` helper along with your `select_tag` to quickly make a list, like this:

```
<%= select_tag(:age, options_for_select([["old", 1], ["old",2]["dead",3]]))
```

Hooray!


###Date and Time

Rails has some nice helper methods built in for populating our dropdowns with dates and times.

We can first choose a 'starting date' to, known as `select_date`, to generate a date from which rails will dynamically generate drop downs. Here is an example:

```
<%= select_date Date.today, prefix :today %>
```

Henceforth (shout out to P.J.), `today` will act as a reference to our established starting point, here semantically known as 'today'. Because this is generated by Ruby, it will change dynamically!

'today' will also give us a hash from params with keys in it like 'year', 'month' and 'date'.

We can use date and time helpers to create objects as well, but I don't quite understand that yet, and am tired. Hopefully I will update this later.
