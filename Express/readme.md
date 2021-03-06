Make sure you are having npm installed on your system with this command
```
npm -v
```
Note : If not, Install npm before proceeding

Create a new directory
```
npm init
```
Provide necessary information here, if you don't know what to fill just press enter after enter. Try to provide as much as information as possible.
This will create a package.json in you folder
```
npm install
```

Install express
```
npm install -g express-generator -save
```

```
IN:express --view=ejs --git
OUT:
 create : public\
   create : public\javascripts\
   create : public\images\
   create : public\stylesheets\
   create : public\stylesheets\style.css
   create : routes\
   create : routes\index.js
   create : routes\users.js
   create : views\
   create : views\error.ejs
   create : views\index.ejs
   create : .gitignore
   create : app.js
   create : package.json
   create : bin\
   create : bin\www

   install dependencies:
     > npm install

   run the app:
     > SET DEBUG=web-project-2:* & npm start

```
Just to make sure, Again install npm on your working directory

```
IN:npm install
OUT:
npm notice created a lockfile as package-lock.json. You should commit this file.
added 53 packages from 38 contributors and audited 141 packages in 4.091s
found 0 vulnerabilities
```
To start server on your folder
```
npm start
```

Then Get out of the terminal using Ctrl+C (Windows).Add version control to your folder.
 To create version control install git and the proceed below

To check whether the git is installed. Type git
```
IN:git
OUT:
usage: git [--version] [--help] [-C <path>] [-c <name>=<value>]
           [--exec-path[=<path>]] [--html-path] [--man-path] [--info-path]
           [-p | --paginate | -P | --no-pager] [--no-replace-objects] [--bare]
           [--git-dir=<path>] [--work-tree=<path>] [--namespace=<name>]
           <command> [<args>]

These are common Git commands used in various situations:

start a working area (see also: git help tutorial)
   clone      Clone a repository into a new directory
   init       Create an empty Git repository or reinitialize an existing one

work on the current change (see also: git help everyday)
   add        Add file contents to the index
   mv         Move or rename a file, a directory, or a symlink
   reset      Reset current HEAD to the specified state
   rm         Remove files from the working tree and from the index

examine the history and state (see also: git help revisions)
   bisect     Use binary search to find the commit that introduced a bug
   grep       Print lines matching a pattern
   log        Show commit logs
   show       Show various types of objects
   status     Show the working tree status

grow, mark and tweak your common history
   branch     List, create, or delete branches
   checkout   Switch branches or restore working tree files
   commit     Record changes to the repository
   diff       Show changes between commits, commit and working tree, etc
   merge      Join two or more development histories together
   rebase     Reapply commits on top of another base tip
   tag        Create, list, delete or verify a tag object signed with GPG

collaborate (see also: git help workflows)
   fetch      Download objects and refs from another repository
   pull       Fetch from and integrate with another repository or a local branch
   push       Update remote refs along with associated objects

'git help -a' and 'git help -g' list available subcommands and some
concept guides. See 'git help <command>' or 'git help <concept>'
to read about a specific subcommand or concept.
```
If succesfully installed, you 'll get output as above

To check git status
```
git status
```

Intialise git in your folder
```
git init
```

Add your files and make it ready to commit
```
git add .
```
 Commit your file
```
git commit -m "First Commit"
```
Again check git status
```
git status
```
Add your credentials using following commands
```
git config --global user.name "Your Name"
git config --global user.email "youremail@someorganistaion.com"
```


Now lets create a simple application
Open app.js file in your working directory

Find the line containing below chunk of code

Find this 
```
var indexRouter = require('./routes/index');
var usersRouter = require('./routes/users');
```
Replace with
```
var router = express.Router();
```
Find this
```
app.use('/', indexRouter);
app.use('/users', usersRouter);
```
Replace with
```
app.use(router);
```
Below this line 
```
var router = express.Router();
```
Add following code
```
var books=[
  {name:'XP Explained',author:'Karl'},
  {name:'XP Explained 2',author:'Karl'}
]

router.get('/',function(req,res,next){
  res.render('index',{title:'Express'});
});

router.get('/books',function(req,res,next){
  res.render('books_view',{count:books.length,books:books});
});
```
Then create a new 'books_view.ejs' file in your working directory.
Paste this code into that file
```
<!DOCTYPE html>
<html>
  <head>
    <title>Books</title>
    <link rel='stylesheet' href='/stylesheets/style.css' />
  </head>
  <body>
    <h1>List of Books (<%= count %>)</h1>
    <% for (book of books){ %>
        <p>
            <%=book.name %>
        </p>

    <% } %>
  </body>
</html>
```
Now start npm server 
```
npm start
```
and go to this url : http://localhost:3000/books
<br/>Your browser will show something like this 
```
List of Books (2)
XP Explained

XP Explained 2
```
Note: Use Ctrl+C to exit from server and npm start to start the server.<br>
Execute all terminal commands after terminating the server.

To check what changes you have made use git diff
```
git diff
```
Note: Press q to exit from git messege

Add your changes to the git
```
git add .
```
Commit your changes into git
```
git commit -m "book_view.ejs creation"
```
Now add more details into our page. Replace this content into the body of book_view.ejs 
```
<h1>List of Books (<%= count %>)</h1>
    <table>
      <tr>
        <th>Name</th>
        <th>Author</th>
        <th>Quantity</th>
        <th>Price</th>
        <th>Description</th>
      </tr>  
      <% for (book of books){ %>
        <tr>
            <td><%=book.name %></td>
            <td><%=book.author %></td>
            <td><%=book.quantity %></td>
            <td><%=book.price %></td>
            <td><%=book.description %></td>
          </tr>
    <% } %>
      </table>
```
Let's do the backend data inputs. Modify the books(list of dictionary) in app.js to something like this 
```
var books=[
  {name:'The Alchemist',author:'Paulo Coelho',price:'₹350',quantity:'120',description:'The Alchemist follows the journey of an Andalusian shepherd boy named Santiago'},
  {name:'Half Girlfriend',author:'Chetan Bhagat',price:'₹350',quantity:'100',description:'Half Girlfriend is an Indian English coming of age, young adult romance novel by Indian author Chetan Bhagat'},
  {name:'2 States',author:'Chetan Bhagat',price:'₹350',quantity:'180',description:'he Story of My Marriage commonly known as 2 States is a 2009 novel written by Chetan Bhagat.'},
]
```
Add some css content to the table that we created. Go to public/stylesheets/style.css and this content.
```
table {
  font-family: arial, sans-serif;
  border-collapse: collapse;
  width: 100%;
}

td, th {
  border: 1px solid #dddddd;
  text-align: left;
  padding: 8px;
}

tr:nth-child(even) {
  background-color: #dddddd;
}
```
Reload the server and go to this url again http://localhost:3000/books
Yaay! We did it

Then what if , we want add data into the existing data on runtime.Let's try that it new ejs file. So create new ejs file 'books_new.ejs'

Copy the content of books_view.ejs into the file we created and replace the content in body with the content below
```
 <h1 style='text-align: center'>Book Store</h1>
    <h1>New Book</h1>
    <form>
        <p>
            <label>Book Name</label>
            <input type="text" name="name">
        </p>

        <p>
            <label>Author</label>
            <input type="text" name="author">
        </p>

        <p>
            <label>Quantity</label>
            <input type="number" name="quantity">
        </p>

        <p>
            <label>Price</label>
            <input type="number" name="price">
        </p>
        <p>
            <label>Description</label>
            <input type="text" name="info">
        </p>
         <p>

            <input type="submit" name="submit">
        </p>
    </form>
```
We need to make changes in app.js inorder to get the data entered the webpage
```

```
