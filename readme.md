# How to convert an Excel table into a searchable HTML table

## tl;dr
Using Excel's Flash Fill feature and [List.js](http://listjs.com/), it's pretty easy to make create a simple, searchable HTML table.

## Uses
HTML tables
List.js - [site](http://listjs.com/) | [on github](https://github.com/javve/list.js)
Semantic UI - [site](https://semantic-ui.com/) | [on github](https://github.com/semantic-org/semantic-ui/)

## Step 1: Flash Fill
**A Note:** I'm told that if you're using a Mac, Flash Fill isn't a feature. [Here is an alternate method](https://www.uwgb.edu/dutchs/CompTips/ExcelHTML.HTM) for custom HTML tables. It's a little more work, but should also do the job.

1. Start with your Excel table.
![An Excel Table](https://i.gyazo.com/63b135a68e6b397cbb4a61262aef5841.png)

2. Write the HTML for the rows and cells for the first row of the table. Make sure to give each column a class. In the example, I have columns for id, project-name, and data.
![Adding HTML](https://i.gyazo.com/157f39454d3d8d29f1b245b52de5289c.gif)

3. Start typing out the HTML for the next line until it auto-fills the rest of the form. Then press enter.
![Flash Filling](https://i.gyazo.com/47eb8af0d9e24abc11c79770d0c679d5.gif)

## Step 2: Setting up List.js and the HTML file
1. In the head of the HTML file include List.js
```html
<script src="https://cdnjs.cloudflare.com/ajax/libs/list.js/1.5.0/list.min.js"></script>
```

2. I'm also using Semantic UI for my styling. So add the following for that. You can of course use something else or custom CSS styling, or no styling if that's how you roll.
```html
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/semantic-ui/2.2.13/semantic.css">
```

3. Create a div, into which you will place your search box, sorting buttons, and table. Give it an id. In the example, I used "projects".
```html
<div id="projects">
</div>
```

4. Inside this div, add a search box with class="search".
```html
<div id="projects">
  <input class="search" placeholder="Search"></input>
</div>
```

5. Also add buttons with class="sort" and data-sort="<column-id>".
```html
<div id="projects">
  <input class="search" placeholder="Search"></input>
  <button class="sort" data-sort="id">Sort by ID</button>
  <button class="sort" data-sort="project-name">Sort by Project Name</button>
  <button class="sort" data-sort="data">Sort by Project Data</button>
</div>
```

6. Start the table. Inside the table include a tbody with class="list"
```html
<table>
  <tbody class="list">
  </tbody>
</table>
```

7. Then copy and paste the code from your Excel table into the HTML table.
![Pasting Table](https://i.gyazo.com/023395b88bddb8b9b3b712e9fe310c67.gif)

8. Finally, at the end of the body add the following script adjusted for your variables. In the valueNames array include the ids of your columns. The second var can be named anything. But the first new List input must be the id for the div in step 3. In this case 'projects'.
```html
<script type='text/javascript'>
  var options = {
    valueNames: ['id', 'project-name', 'data']
  };

  var projects = new List('projects', options);
</script>
```

9. That's pretty much it. Style it the way you want. Open the file in your browser and see it in action.
![Sort and Search in Action](https://i.gyazo.com/42735a81ed2623bbbf6ed1da7196cf93.gif)
