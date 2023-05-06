Download Link: https://assignmentchef.com/product/solved-eecs485-p1-templated-static-site-generator
<br>
<h1>Introduction</h1>

An Instagram clone implemented with a templated static site generator. This is the first of an EECS 485 three project sequence: a static site generator from templates, server-side dynamic pages, and client-side dynamic pages.

The learning goals of this project include HTML, CSS, templates, Python programming, and basic shell scripting. It is also a “readiness test” that will give you an idea of what EECS 485 will be like.

Write a Python program that takes as input HTML templates, JSON data and misc. static files (like images and CSS) and generates as output a web site of static content. Then, use your new tool to build a non-interactive website. <a href="https://jekyllrb.com/">Jekyll</a> and <a href="https://www.fullstackpython.com/pelican.html">Pelican</a> are two examples of open source static site generators.

Here’s a preview of what your finished project will look like. <sub>insta485generator</sub> is the name of the Python program you will write. <sub>insta485</sub> is an input directory containing HTML templates, JSON data and misc. static files (like images and CSS). <sub>insta485/html</sub> is an output directory containing generated static HTML files.

$ insta485generator insta485

$ cd insta485/html/

$ python3 -m http.server 8000

Serving HTTP on 0.0.0.0 port 8000 (http://0.0.0.0:8000/) …

Then you will navigate to <a href="http://localhost:8000/">http://localhost:8000</a> and see the non-interactive website that you created.

If you’re new to HTML, CSS and Python, here are some helpful resources:

<a href="https://www.w3schools.com/html/html_intro.asp">W3 Schools Beginner’s Guide to HTML</a>

<a href="https://www.w3schools.com/html/html_css.asp">W3 Schools CSS</a>

<a href="https://docs.python.org/3/tutorial/index.html">Python 3 Tutorial</a>

This spec will walk you through these parts:

<ol>

 <li>Setting up your computer</li>

 <li>Hand coded HTML</li>

 <li>Creating Python starter files</li>

 <li><sub>insta485generator</sub> specification</li>

 <li>Static Templated Insta485 specification</li>

 <li>Submitting and grading</li>

 <li>FAQ</li>

</ol>

<h1>Setting up your computer</h1>

We’ll walk you through setting up your operating system, Python virtual environment and version control.

<h2>Operating System</h2>

Set up your computer for local development using the <a href="https://eecs485staff.github.io/p1-insta485-static/setup_os.html">Operating System Tutorial</a><a href="https://eecs485staff.github.io/p1-insta485-static/setup_os.html">.</a>

You should now have a folder for your project. Your folder location might be different.

$ pwd

/Users/awdeorio/src/eecs485/p1-insta485-static

<h2>Version Control</h2>

Set up version control using the <a href="https://eecs485staff.github.io/p1-insta485-static/setup_git.html">Version control tutorial</a>.

After you’re done, you should have a local repository with a “clean” status and your local repository should be connected to a remote GitLab repository.

$ pwd

/Users/awdeorio/src/eecs485/p1-insta485-static

$ git status

On branch master

Your branch is up-to-date with ‘origin/master’.

nothing to commit, working tree clean

$ git remote -v origin https://gitlab.eecs.umich.edu/awdeorio/p1-insta485-static.git (fetch) origin https://gitlab.eecs.umich.edu/awdeorio/p1-insta485-static.git (push) You should have a <sub>.gitignore</sub> file (<a href="https://eecs485staff.github.io/p1-insta485-static/setup_git.html#add-a-gitignore-file">instructions</a>).

$ pwd

/Users/awdeorio/src/eecs485/p1-insta485-static

$ head .gitignore

This is a sample .gitignore file that’s useful for EECS 485 projects.

<em>… </em>

<h2>Python virtual environment</h2>

Create a Python virtual environment for project 1 using the <a href="https://eecs485staff.github.io/p1-insta485-static/setup_virtual_env.html">Python Virtual Environment Tutorial</a>.

You should now have Python tools installed locally.

$ pwd

/Users/awdeorio/src/eecs485/p1-insta485-static

$ ls env

$ source env/bin/activate

$ which python

/Users/awdeorio/src/eecs485/p1-insta485-static/env/bin/python

$ which pip

/Users/awdeorio/src/eecs485/p1-insta485-static/env/bin/pip

<strong>Python debugger</strong>

Learn how to use the Python debugger, <sub>pdb</sub> using the <a href="https://eecs485staff.github.io/p1-insta485-static/setup_pdb.html">Python Debugging Tutorial</a>.

<strong>Browser tutorial</strong>

Learn about the developer tools built into your browser with the <a href="https://eecs485staff.github.io/p1-insta485-static/setup_browser.html">Browser Tutorial</a>.

<h2>Starter files</h2>

Download and unpack the starter files.

$ pwd

/Users/awdeorio/src/eecs485/p1-insta485-static

$ wget https://eecs485staff.github.io/p1-insta485-static/starter_files.tar.gz $ tar -xvzf starter_files.tar.gz

Move the starter files to your project directory and remove the original <sub>starter_files/ </sub>directory.

$ pwd

/Users/awdeorio/src/eecs485/p1-insta485-static

$ mv starter_files/<strong>*</strong> .

$ rm -rf starter_files starter_files.tar.gz You should see these files.

$ tree

<em>. </em>

├── VERSION

├── hello

│   ├── config.json

│   └── templates

│       └── index.html

├── hello_css

│   ├── config.json

│   ├── static

│   │   └── css

│   │       └── style.css

│   └── templates

│       └── index.html

├── insta485

│   ├── config.json │   └── static

│       └── uploads

<em>            … </em>

│           └── e1a7c5c32973862ee15173b0259e3efdb6a391af.jpg

├── setup.py └── tests

<em>    … </em>

└── util.py

<table width="600">

 <tbody>

  <tr>

   <td width="218">VERSION</td>

   <td width="382">Version of the starter files</td>

  </tr>

  <tr>

   <td width="218">hello/</td>

   <td width="382">Sample input for insta485generator</td>

  </tr>

  <tr>

   <td width="218">hello_css/</td>

   <td width="382">Sample input for insta485generator</td>

  </tr>

  <tr>

   <td width="218">insta485/</td>

   <td width="382"><a href="https://eecs485staff.github.io/p1-insta485-static/static-templated-insta485-specification">Static templated Insta485</a> goes here</td>

  </tr>

  <tr>

   <td width="218">insta485/config.json</td>

   <td width="382">Data for future Insta485 templates</td>

  </tr>

  <tr>

   <td width="218">insta485/static/uploads/</td>

   <td width="382">Sample images for Insta485</td>

  </tr>

  <tr>

   <td width="218">setup.py</td>

   <td width="382">insta485generator python package configuration</td>

  </tr>

  <tr>

   <td width="218">tests/</td>

   <td width="382">Public unit tests</td>

  </tr>

 </tbody>

</table>

Before making any changes to the clean starter files, it’s a good idea to make a commit to your Git repository.

<h1>Hand coded HTML</h1>

Once you have your computer set up, you’ll write two HTML files by hand: <sub>html/index.html</sub> and html/u/awdeorio/index.html . This will give you practice with HTML and CSS, which you’ll later

generate using Python code.

For those developing locally, navigate to your project’s root directory. Also, remember to activate your Python virtual environment every time you begin a coding sessions (AKA start a new shell).

$ pwd

/Users/awdeorio/src/eecs485/p1-insta485-static

$ source env/bin/activate

Create a directory layout using <sub>mkdir </sub>. The image <sub>logo.png</sub> is optional; you can style your website however you like. Here are some commands to get you started.

$ pwd

/Users/awdeorio/src/eecs485/p1-insta485-static

$ mkdir html/

$ mkdir html/css/

$ mkdir html/images/

$ mkdir html/u/

$ mkdir html/u/awdeorio/

$ mkdir html/uploads/

$ touch html/css/style.css  <em># touch creates empty files</em>

$ touch html/index.html

$ touch html/u/awdeorio/index.html

$ cp insta485/static/uploads/<strong>*</strong> html/uploads/

Add the initial file structure to the git repo.

Here are the files you should have when you are done.

$ pwd

/Users/awdeorio/src/eecs485/p1-insta485-static

$ tree html/ html/

├── css

│   └── style.css

├── images

├── index.html

├── u

│   └── awdeorio

│       └── index.html

└── uploads

├── 122a7d27ca1d7420a1072f695d9290fad4501a41.jpg

├── 2ec7cf8ae158b3b1f40065abfb33e81143707842.jpg

├── 505083b8b56c97429a728b68f31b0b2a089e5113.jpg

├── 5ecde7677b83304132cb2871516ea50032ff7a4f.jpg

├── 73ab33bd357c3fd42292487b825880958c595655.jpg

├── 9887e06812ef434d291e4936417d125cd594b38a.jpg

├── ad7790405c539894d25ab8dcf0b79eed3341e109.jpg

└── e1a7c5c32973862ee15173b0259e3efdb6a391af.jpg

Start your two HTML files ( html/index.html and html/u/awdeorio/index.html ) like this. Edit HTML files with a text editor.

<strong>&lt;!DOCTYPE html&gt;</strong>

&lt;html lang=”en”&gt;

Hello world!

&lt;/html&gt;

Run a test server and browse to <a href="http://localhost:8000/">http://localhost:8000/</a> where you will see “hello world”. Again, recall that this is a <em>static file server</em>, which serves copies of files from the server’s file system. In this example, the file is a plain text file containing HTML.

$ pwd

/Users/awdeorio/src/eecs485/p1-insta485-static

$ cd html/

$ python3 -m http.server 8000

Serving HTTP on 0.0.0.0 port 8000 (http://0.0.0.0:8000/) …

Keep up your good <sub>git</sub> habits by committing files when you’ve completed each small task.

Continue working on <sub>html/index.html </sub>. When you’re done, the page should have the following content, although yours might look different. For example, a logo is not required. To be clear: there are no autograder tests for your CSS layout. You can make it look however you want. What you must include is the text, images, and links shown in the screenshot below. For details on what links to include, see the All pages and Index sections. You may have to reference your

config.json file to figure out what URLs some links may lead to (it’s okay if some lead to

nowhere for this hand-coded portion). Don’t forget to <sub>git add</sub> and <sub>git commit</sub> when you’re done.

Next, code <sub>html/u/awdeorio/index.html </sub>. When you’re done, the page should have the following content, although yours might have different styling. Again, we’re not requiring any particular

CSS styling. See the <sub>/u/&lt;user_url_slug&gt;/</sub> section for more details about the links to include. Don’t forget to <sub>git add</sub> and <sub>git commit</sub> when you’re done.

All HTML should be <a href="https://w3c.github.io/developers/tools/">W3C HTML5 compliant</a>. Here’s how to check yours at the command line.

$ pwd

/Users/awdeorio/src/eecs485/p1-insta485-static $ html5validator –root html/

<h2>Test</h2>

Run the public autograder testcases on your hand coded HTML.

$ pytest -v tests/test_handcoded_html.py tests/test_handcoded_index.py tests/test_handcode

<em>… </em>

========================== 12 passed in 3.76 seconds ===========================

<h1>Creating the Python starter files</h1>

This section will help you get your Python files set up.

Our program will be called <sub>insta485generator </sub>. The following steps will help you to create a Python package for it. (More info in the <a href="https://docs.python.org/3/tutorial/modules.html">Python documentation on modules</a>, especially the <a href="https://docs.python.org/3/tutorial/modules.html#packages">section on packages</a>.

$ pwd

/Users/awdeorio/src/eecs485/p1-insta485-static

$ mkdir insta485generator/

$ cd insta485generator/

All Packages must have an <sub>__init__.py</sub> file. Our starter package is simple, so it won’t do anything. Create the file <sub>insta485generator/__init__.py</sub> (be sure to include the 2 underscores before and after init) and add a comment like this to it:

“””A static site generator.”””

Now within the insta485generator directory, create a new file called <sub>__main__.py </sub>. Our main function will go in <sub>insta485generator/__main__.py </sub>. We have given you the skeleton code below.

“””Build static HTML site from directory of HTML templates and plain files.”””

<strong>def</strong> <strong>main</strong>():

“””Top level command line interface.”””     <strong>print</strong>(“Hello world!”)

<strong>if</strong> __name__ <strong>==</strong> “__main__”:     main()

Now, try running it:

$ python3 insta485generator/__main__.py Hello world!

Next, we’ll install our package into our development environment. Double-check that the development environment is still active. If it’s not, then activate it with <sub>source env/bin/activate </sub>.

$ echo $VIRTUAL_ENV

/Users/awdeorio/src/p1-insta485-static/solution/awdeorio/env

The <sub>setup.py</sub> file provided with the starter files describes how your package should be installed. We’ve included some libraries that will be helpful later. You are not allowed to add any additional <a href="https://chriswarrick.com/blog/2014/09/15/python-apps-the-right-way-entry_points-and-scripts/">dependencies other than the ones that we specify. More info about </a><a href="https://chriswarrick.com/blog/2014/09/15/python-apps-the-right-way-entry_points-and-scripts/">setup scripts</a><a href="https://chriswarrick.com/blog/2014/09/15/python-apps-the-right-way-entry_points-and-scripts/"> and </a><a href="https://chriswarrick.com/blog/2014/09/15/python-apps-the-right-way-entry_points-and-scripts/">Python entry points</a><a href="https://chriswarrick.com/blog/2014/09/15/python-apps-the-right-way-entry_points-and-scripts/">.</a>

At this point, we’ve got these files (excluding <sub>env </sub>, <sub>__pycache__</sub> and <sub>html </sub>):

$ tree insta485generator –matchdirs -I __pycache__ insta485generator ├── __init__.py

└── __main__.py

We can now use <sub>pip</sub> to install <sub>insta485generator</sub> package using <sub>setup.py </sub>. We’ll install in editable mode so that we won’t have to reinstall when we make changes to our Python source code. Again, be sure that your virtual envirnment is active.

$ echo $VIRTUAL_ENV

/Users/awdeorio/src/p1-insta485-static/solution/awdeorio/env

$ pip install -e .

<em>  … </em>

Running setup.py develop for insta485generator Successfully installed … insta485generator …

Because of the entry point in setup.py ( ‘insta485generator =

insta485generator.__main__:main’ ), there’s now an executable that calls our insta485generator package’s <sub>main()</sub> function!

$ insta485generator Hello world!

How did it do that? When you activate your virtual environment with <sub>source env/bin/activate </sub>, your shell’s <sub>PATH</sub> environment variable is temporarily modified to include programs installed to ./env/bin/ . Prove it to yourself:

$ echo $PATH

/Users/awdeorio/src/p1-insta485-static/solution/awdeorio/env/bin:/usr/local/bin:/usr/local $ which insta485generator

/Users/awdeorio/src/p1-insta485-static/solution/awdeorio/env/bin/insta485generator

When you get this working, it may be a good point to commit to git




### `pytest` utility

Learn how to use the Python `pytest` unit test utility using the [`pytest` Tutorial](setup Now you can continue developing `insta485generator` by adding code to `insta485generator/_







# `insta485generator` specification

We will now begin implementing the functionality for our insta485generator. We will modify




<ul>

 <li>Handle command line arguments using the [click library](https://click.palletsprojects.c</li>

 <li>Render the provided templates and write them to output files and create all the necessa</li>

 <li>Copy over a static directory if it is provided</li>

 <li>Handle errors</li>

</ul>




The inputs to `insta485generator` are templated HTML files with data in JSON format.  The




We have provided two examples to help you get your `insta485generator` working. We recomme




The command line utility supports the following options.  Hint: use the [click library](ht

“`console

$ insta485generator

Usage: insta485generator [OPTIONS] INPUT_DIR

Try “insta485generator –help” for help.




Error: Missing argument “INPUT_DIR”.

$ insta485generator –help

Usage: insta485generator [OPTIONS] INPUT_DIR




Templated static website generator.




Options:

-v, –verbose  Print more output.

–help         Show this message and exit.

The configuration for one website is an input directory containing a data file ( <sub>config.json </sub>), a templates/ directory and an optional <sub>static/</sub> directory. Templates are rendered and written to

output files, and static files are copied without modification.

We will now walk through the hello example. The <sub>hello/</sub> example is provided with the starter files.

$ tree hello/

<em>. </em>

├── config.json

└── templates

└── index.html

A configuration file (e.g., <sub>hello/config.json </sub>) is a JSON string with a list of dictionaries. Each dictionary contains a <sub>url </sub>, the name of a <sub>template</sub> file and a <sub>context</sub> dictionary. The <sub>template </sub>file is rendered using the <sub>context</sub> dictionary. Hint: Python has a built in <a href="https://docs.python.org/3/library/json.html">JSON library</a><a href="https://docs.python.org/3/library/json.html">.</a>

[

{

<strong>“url”</strong>: “/”,

<strong>“template”</strong>: “index.html”,

<strong>“context”</strong>: {

<strong>“words”</strong>: [

“hello”,

“world”

]

}

}

]

Templates use jinja2 syntax, for example hello/templates/index.html below. Hint: check out the <a href="http://jinja.pocoo.org/">Jinja2 library</a>.

<strong>&lt;!DOCTYPE html&gt;</strong>

&lt;html lang=”en”&gt;

&lt;head&gt;&lt;title&gt;Hello world&lt;/title&gt;&lt;/head&gt;

&lt;body&gt;

{% for word in words %}

{{word}}

{% endfor %}

&lt;/body&gt;

&lt;/html&gt;




Running <sub>insta485generator INPUT_DIR</sub> renders templates, copying the results to an output directory. The output directory is <sub>${INPUT_DIR}/html </sub>, where <sub>${INPUT_DIR}</sub> is the command line argument INPUT_DIR .

After you finish <sub>insta485generator </sub>, it will render templates and create directories like this example.

$ tree hello hello

├── config.json

└── templates

└── index.html

$ insta485generator hello

$ tree hello hello

├── config.json

├── html

│   └── index.html └── templates

└── index.html

Output files rendered from templates no longer contain any template code, for example hello/html/index.html . The algorithm for an output filename is os.path.join(input_dir,

“html”, url.lstrip(“/”), “index.html”) where input_dir is the command line argument INPUT_DIR and url is the URL read from the config.json file.

<strong>&lt;!DOCTYPE html&gt;</strong>

&lt;html lang=”en”&gt;

&lt;head&gt;&lt;title&gt;Hello world&lt;/title&gt;&lt;/head&gt;

&lt;body&gt;  hello  world

&lt;/body&gt;

Finally, serve up the newly created site and browse to <a href="http://localhost:8000/">http://localhost:8000/</a><a href="http://localhost:8000/">.</a>

$ cd hello/html/

$ python3 -m http.server 8000

Serving HTTP on 0.0.0.0 port 8000 (http://0.0.0.0:8000/) …

We’ve published the <sub>test_hello</sub> autograder testcase. After copying the <sub>test</sub> directory from the starter files to your working directory, you can run it yourself like this:

$ pytest -v tests/test_hello.py

============================= test session starts ==============================

<em>… </em>




::TestHello::test_files PASSED                                           [ 50%] ::TestHello::test_index PASSED                                           [100%]

=========================== 2 passed in 0.59 seconds ===========================

<h2>More examples</h2>

Here’s an example of the <sub>–verbose</sub> option. The position of the option doesn’t matter.

$ rm -rf hello/html

$ insta485generator hello –verbose

Rendered index.html -&gt; hello/html/index.html

Here’s a slightly more complicated example with a static CSS style file. The <sub>hello_css/</sub> example is provided with the starter files.

$ tree hello_css hello_css ├── config.json

├── static

│   └── css

│       └── style.css

└── templates

└── index.html

This is the config file hello_css/config.json :

[

{

<strong>“url”</strong>: “/”,

<strong>“template”</strong>: “index.html”,

<strong>“context”</strong>: {

<strong>“words”</strong>: [

“hello”,

“world”

]

}

}

]

Here’s hello_css/templates/index.html :

<strong>&lt;!DOCTYPE html&gt;</strong>

&lt;html lang=”en”&gt;

&lt;head&gt;

&lt;title&gt;Hello world&lt;/title&gt;

&lt;link rel=”stylesheet” type=”text/css” href=”/css/style.css”&gt;

&lt;/head&gt;

&lt;body&gt;

{% for word in words %}

&lt;div class=”important”&gt;{{word}}&lt;/div&gt;

{% endfor %}

&lt;/body&gt;

&lt;/html&gt;




And hello_css/static/css/style.css :

body {

<strong>background</strong>: pink;

}

div<strong>.important</strong> {     <strong>font-weight</strong>: bold;     <strong>font-size</strong>: 1000%;

}

Build and list output files

$ insta485generator -v hello_css

Copied hello_css/static/ -&gt; hello_css/html/

Rendered index.html -&gt; hello_css/html/index.html

$ tree hello_css/html hello_css/html ├── css

│   └── style.css └── index.html

We’ve published the <sub>test_hello_css</sub> autograder testcase. You can run it yourself like this:

$ pytest -v tests/test_hello_css.py

============================= test session starts ==============================

<em>… </em>




::TestHelloCSS::test_css_dir PASSED                                      [ 33%]

::TestHelloCSS::test_files PASSED                                        [ 66%] ::TestHelloCSS::test_index PASSED                                        [100%]

=========================== 3 passed in 0.59 seconds ===========================

<h2>A few notes about the jinja2 library</h2>

We’d like to save you a bit of frustration getting the <sub>jinja2</sub> library working the same way our instruction solution works. First, in order to make <a href="http://jinja.pocoo.org/docs/2.9/templates/#template-inheritance">template inheritance</a> work correctly, you’ll need to use the <a href="http://jinja.pocoo.org/docs/2.9/api/#jinja2.FileSystemLoader"><sub>FileSystemLoader</sub></a> <a href="http://jinja.pocoo.org/docs/2.9/api/#jinja2.FileSystemLoader">.</a> Second, we’re going to <a href="http://jinja.pocoo.org/docs/2.9/api/">enable auto escaping</a> for security reasons.

Here’s how we configured out template environment in our instructor solution:

template_env = jinja2.Environment(

loader=jinja2.FileSystemLoader(template_dir),     autoescape=jinja2.select_autoescape([‘html’, ‘xml’]), )

<h2>Python code style</h2>

Verify that your Python code conforms the <a href="https://www.python.org/dev/peps/pep-0008/">PEP 8 Style Guide for Python</a>. Check for common Python errors and additional style guidelines using <a href="https://www.pylint.org/">Pylint</a>. Confirm that internal documentation (comments) conforms to the <a href="https://www.python.org/dev/peps/pep-0257/">PEP 257 Docstring Conventions</a>.

$ pip install pycodestyle pydocstyle pylint

$ pycodestyle setup.py insta485generator

$ pylint –disable<strong>=</strong>no-value-for-parameter setup.py insta485generator

No config file found, using default configuration




——————————————————————– Your code has been rated at 10.00/10 (previous run: 10.00/10, +0.00)

$ pydocstyle setup.py insta485generator

<strong>HINT</strong> test your style frequently. It’s hard to fix the style of a large code base with many errors. Later, we’ll automate these tests with a script ( <sub>insta485test </sub>). Remember when you were first learning to code in C/C++? Did you ever see a classmate code their entire project, and then say “OK, now all I have to do is compile it!”. Bad idea! Just like C/C++ compilation, check your code in small increments.

<h2>Test</h2>

Run the public autograder testcases on your <sub>insta485generator </sub>.

$ pytest tests/test_hello.py tests/test_hello_css.py

<em>… </em>

=========================== 5 passed in 1.14 seconds ===========================

<h1>Static Templated Insta485 specification</h1>

In this part of the project, you will write HTML template files that you can render using insta485generator to create a non-interactive Instagram clone. First, this section will help you

create skeleton files. Then, in the URLs section, we’ll describe each page in detail and provide a screen shot.

First, set up the directory structure using <sub>mkdir</sub> and the provided starter files. Use your handcoded HTML files earlier in the project as a starting point. Put the HTML files in

insta485/templates/index.html and insta485/templates/user.html . When you’re done, you

should have a new directory called <sub>insta485</sub> that looks like this:

$ tree insta485 insta485

├── config.json

├── static

│   ├── css

│   │   └── style.css

│   ├── images

│   │   └── logo.png

│   └── uploads

│       ├── 122a7d27ca1d7420a1072f695d9290fad4501a41.jpg

│       ├── 2ec7cf8ae158b3b1f40065abfb33e81143707842.jpg

│       ├── 505083b8b56c97429a728b68f31b0b2a089e5113.jpg

│       ├── 5ecde7677b83304132cb2871516ea50032ff7a4f.jpg

│       ├── 73ab33bd357c3fd42292487b825880958c595655.jpg

│       ├── 9887e06812ef434d291e4936417d125cd594b38a.jpg

│       ├── ad7790405c539894d25ab8dcf0b79eed3341e109.jpg │       └── e1a7c5c32973862ee15173b0259e3efdb6a391af.jpg

└── templates

├── index.html

└── user.html

A few things to note. First, <sub>images/logo.png</sub> is optional. You are welcome to create any logo you want, or to omit it and use plain text. Second, remember that everything inside insta485/static/ will be copied to insta485/html/ by insta485generator . Also note that the config.json should come from the starter code, you do not have to write this by hand.

Use <sub>insta485generator</sub> to render the templates and copy the static files. Yea, yea, our HTML files don’t have any Jinja2 syntax in them, but they’re still valid template files!

$ rm -rf ‘insta485/html’

$ insta485generator insta485

Error_Jinja: jinja2 template following.html

TemplateNotFound: following.html

We’re getting an error because the provided <sub>insta485/config.json</sub> contains configurations for URLs that we haven’t written templates for. Let’s create a temporary configuration that’s shorter. First back up the old one.

$ cp -v insta485/config.json insta485/config.json.bak

‘insta485/config.json’ -&gt; ‘insta485/config.json.bak’

Then, edit <sub>insta485/config.json</sub> so that it only contains configurations for URLs that use the index.html and <sub>user.html</sub> templates. Be careful, JSON doesn’t allow trailing commas!

[

{

<strong>“url”</strong>: “/”,

<strong>“template”</strong>: “index.html”,

<strong>“context”</strong>: {

<strong>“logname”</strong>: “awdeorio”,       <strong>“posts”</strong>: [

…

]

}   },   …

{

<strong>“url”</strong>: “/u/michjc/”,

<strong>“template”</strong>: “user.html”,     <strong>“context”</strong>: {

…

}

}

]

Now, try running <sub>insta485generator</sub> again. Start a development server and you’ll see the rendered templates, which at this point are just copies of your hand coded HTML files.

$ pwd

/Users/awdeorio/src/eecs485/p1-insta485-static

$ rm -rf insta485/html

$ insta485generator insta485 -v

Copied insta485/static/ -&gt; insta485/html/

Rendered index.html -&gt; insta485/html/index.html

Rendered user.html -&gt; insta485/html/u/awdeorio/index.html

Rendered user.html -&gt; insta485/html/u/jflinn/index.html Rendered user.html -&gt; insta485/html/u/jag/index.html

Rendered user.html -&gt; insta485/html/u/michjc/index.html

$ cd insta485/html/

$ python3 -m http.server 8000

Serving HTTP on 0.0.0.0 port 8000 (http://0.0.0.0:8000/) …

<em>… </em>$ cd ../../

<h2>Utility scripts</h2>

During development, we’re going to be regenerating this website <em>a lot</em>. Web developers often use short shell scripts to make their lives easier. First, complete the <a href="https://eecs485staff.github.io/p1-insta485-static/setup_scripting.html">Shell Scripting Tutorial</a>.

Write a script to clean up the automatically generated <sub>insta485/html/</sub> directory, build the static site using <sub>insta485generator </sub>, and start a development server on port 8000. We’ll give you the solution here for <sub>bin/insta485run </sub>. Create a folder called <sub>bin</sub> and copy the following code into a file called <sub>insta485run</sub> (note no file extension).

<em>#!/bin/bash</em>

<em># # insta485run</em>

<em># # Clean, build and start server</em>

<em>#</em>

<em># Andrew DeOrio &lt;<a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="5f3e283b3a302d36301f2a32363c37713a3b2a">[email protected]</a>&gt;</em>







<em># Stop on errors, print commands # See https://vaneyckt.io/posts/safer_bash_scripts_with_set_euxo_pipefail/ </em>set -Eeuo pipefail

set -x  <em># Clean</em>

rm -rf insta485/html

<em># Build</em>

insta485generator insta485

<em># Serve </em>cd insta485/html python3 -m http.server 8000

Now, make the script executable so you can use it like a command.

$ pwd

/Users/awdeorio/src/eecs485/p1-insta485-static

$ chmod +x bin/insta485run

$ ./bin/insta485run

+ rm -rf insta485/html/css insta485/html/index.html insta485/html/u

+ insta485generator insta485

+ cd insta485/html

+ python3 -m http.server 8000

Serving HTTP on 0.0.0.0 port 8000 (http://0.0.0.0:8000/) …

Check for <a href="https://eecs485staff.github.io/p1-insta485-static/setup_scripting.html#shell-script-pitfalls">shell script pitfalls</a><a href="https://eecs485staff.github.io/p1-insta485-static/setup_scripting.html#shell-script-pitfalls">.</a>

<h3>insta485test script</h3>

Write another script called <sub>bin/insta485test</sub> that does the following things in this order:

<ol>

 <li>Stops on errors and prints commands</li>

 <li>Runs all unit tests using <sub>pytest tests/</sub></li>

 <li>Runs pycodestyle insta485generator</li>

 <li>Runs pydocstyle insta485generator</li>

 <li>Runs pylint –disable=no-value-for-parameter setup.py insta485generator</li>

 <li>Cleans up a previous <sub>insta485/html</sub> directory</li>

 <li>Builds a new insta485/html directory using insta485generator</li>

 <li>Validates hand-coded HTML in html/ using html5validator ( html5validator –ignore</li>

</ol>

JAVA_TOOL_OPTIONS –root html )

<ol start="9">

 <li>Validates generated HTML in insta485/html/ using html5validator ( html5validator -ignore JAVA_TOOL_OPTIONS –root insta485/html )</li>

</ol>

<h3>Progress so far</h3>

Here’s a complete list of the files in our project up to this point. Note that it excludes <sub>env</sub> and

__pycache__ . This will differ from your final tree because it is missing the templates we will create in the next step.

$ pwd

/Users/awdeorio/src/eecs485/p1-insta485-static

$ tree –matchdirs -I ‘env|__pycache__|*.egg-info’

<em>. </em>

├── bin

│   ├── insta485run

│   └── insta485test

├── html

│   ├── css

│   │   └── style.css

│   ├── images

│   │   └── logo.png

│   ├── index.html

│   ├── u

│   │   └── awdeorio

│   │       └── index.html

│   └── uploads

│       ├── 122a7d27ca1d7420a1072f695d9290fad4501a41.jpg

│       ├── 2ec7cf8ae158b3b1f40065abfb33e81143707842.jpg

│       ├── 505083b8b56c97429a728b68f31b0b2a089e5113.jpg

│       ├── 5ecde7677b83304132cb2871516ea50032ff7a4f.jpg

│       ├── 73ab33bd357c3fd42292487b825880958c595655.jpg

│       ├── 9887e06812ef434d291e4936417d125cd594b38a.jpg

│       ├── ad7790405c539894d25ab8dcf0b79eed3341e109.jpg

│       └── e1a7c5c32973862ee15173b0259e3efdb6a391af.jpg

├── insta485

│   ├── config.json

│   ├── config.json.bak

│   ├── html

│   │   ├── css

│   │   │   └── style.css

│   │   ├── images

│   │   │   └── logo.png

│   │   ├── index.html

│   │   ├── u

│   │   │   ├── awdeorio

│   │   │   │   └── index.html │   │   │   ├── jag

│   │   │   │   └── index.html │   │   │   ├── jflinn

│   │   │   │   └── index.html │   │   │   └── michjc

│   │   │       └── index.html

│   │   └── uploads

│   │       ├── 122a7d27ca1d7420a1072f695d9290fad4501a41.jpg

│   │       ├── 2ec7cf8ae158b3b1f40065abfb33e81143707842.jpg

│   │       ├── 505083b8b56c97429a728b68f31b0b2a089e5113.jpg

│   │       ├── 5ecde7677b83304132cb2871516ea50032ff7a4f.jpg

│   │       ├── 73ab33bd357c3fd42292487b825880958c595655.jpg

│   │       ├── 9887e06812ef434d291e4936417d125cd594b38a.jpg

│   │       ├── ad7790405c539894d25ab8dcf0b79eed3341e109.jpg

│   │       └── e1a7c5c32973862ee15173b0259e3efdb6a391af.jpg

│   ├── static

│   │   ├── css

│   │   │   └── style.css

│   │   ├── images

│   │   │   └── logo.png

│   │   └── uploads

│   │       ├── 122a7d27ca1d7420a1072f695d9290fad4501a41.jpg

│   │       ├── 2ec7cf8ae158b3b1f40065abfb33e81143707842.jpg

│   │       ├── 505083b8b56c97429a728b68f31b0b2a089e5113.jpg

│   │       ├── 5ecde7677b83304132cb2871516ea50032ff7a4f.jpg

│   │       ├── 73ab33bd357c3fd42292487b825880958c595655.jpg

│   │       ├── 9887e06812ef434d291e4936417d125cd594b38a.jpg

│   │       ├── ad7790405c539894d25ab8dcf0b79eed3341e109.jpg │   │       └── e1a7c5c32973862ee15173b0259e3efdb6a391af.jpg

│   └── templates

│       ├── index.html

│       └── user.html

├── insta485generator

│   ├── __init__.py

│   └── __main__.py

├── setup.py

└── tests

├── test_hello.py

└── test_hello_css.py

<h2>URLs</h2>

Now, write templates for each type of URL. You are welcome to add extra files, for example, if you’d like to use <a href="http://jinja.pocoo.org/docs/2.9/templates/#template-inheritance">template inheritance</a>. Style the pages any way you like.

List of URLs and templates:

/ -&gt; index.html

/u/&lt;user_url_slug&gt;/ -&gt; user.html

/u/&lt;user_url_slug&gt;/followers/ -&gt; followers.html /u/&lt;user_url_slug&gt;/following/ -&gt; following.html

/p/&lt;postid_slug&gt;/ -&gt; post.html

/explore/ -&gt; explore.html

<h3>All pages</h3>

Include a link to <sub>/</sub> in the upper left hand corner.

Include a link to /explore/ and /u/&lt;logged_in_user&gt;/ in the upper right hand corner.

Include &lt;title&gt;insta485&lt;/title&gt; . Nothing else should be in the &lt;title&gt; section

<h3>Index /</h3>

<a href="https://eecs485staff.github.io/p1-insta485-static/images/screenshot-index.png">screenshot</a>

All posts from other users that the logged in user is following (including their own). The logged in user is specified by <sub>logname</sub> in <sub>config.json </sub>. The posts are in the order that they appear in the JSON config file. For each post:

Link to the post detail page <sub>/p/&lt;postid_slug&gt;/</sub> by clicking on the timestamp.

Link to the post owner’s page <sub>/u/&lt;user_url_slug&gt;/</sub> by clicking on their username or profile picture.

Time since the post was created

Number of likes, using correct English

Comments, with owner’s username, in the order that they appear in the JSON config file.

Link to the comment owner’s page <sub>/u/&lt;user_url_slug&gt;/</sub> by clicking on their username. Actual image corresponding to the post.

Here’s an example of correct English for number of likes “0 likes”, “1 like”, “2 likes”. The same plural rules apply to number of posts, likes, and followers. Following is always the same “0 following”, “1 following”, “2 following”.

<h4>/u/&lt;user_url_slug&gt;/</h4>

<a href="https://eecs485staff.github.io/p1-insta485-static/images/screenshot-u-awdeorio.png">screenshot 1</a>, <a href="https://eecs485staff.github.io/p1-insta485-static/images/screenshot-u-jag.png">screenshot 2</a>, <a href="https://eecs485staff.github.io/p1-insta485-static/images/screenshot-u-jflinn.png">screenshot 3</a>, <a href="https://eecs485staff.github.io/p1-insta485-static/images/screenshot-u-michjc.png">screenshot 4</a>

Be sure to include

username ( user_url_slug )

Relationship

“following” if the logged in user is following <sub>user_url_slug</sub>

“not following” if the logged in user is not following <sub>user_url_slug</sub>

Blank if logged in user == <sub>user_url_slug</sub>

Number of posts, with correct English

Number of followers, with correct English

Link to /u/&lt;user_url_slug/followers/ Number following

Link to /u/&lt;user_url_slug/following/

Name

A small image for each post

Clicking on the image links to /p/&lt;postid_url_slug&gt;/

<h4>/u/&lt;user_url_slug&gt;/followers/ <a href="https://eecs485staff.github.io/p1-insta485-static/images/screenshot-u-awdeorio-followers.png">screenshot</a></h4>

List the users that are following <sub>user_url_slug </sub>. For each, include:

Icon

Username, with link to <sub>/u/&lt;username&gt;/</sub>

Relationship to logged in user

“following” if logged in user is following username

“not following” if logged in user is not following username Blank if logged in user == username

<h4>/u/&lt;user_url_slug&gt;/following/ <a href="https://eecs485staff.github.io/p1-insta485-static/images/screenshot-u-awdeorio-following.png">screenshot</a></h4>

List the users that <sub>user_url_slug</sub> is following. For each, include:

Icon

Username, with link to <sub>/u/&lt;username&gt;/</sub>

Relationship to logged in user

“following” if logged in user is following username

“not following” if logged in user is not following username Blank if logged in user == username

<strong>/explore/ </strong><a href="https://eecs485staff.github.io/p1-insta485-static/images/screenshot-explore.png">screenshot</a>

This page lists all users that the logged in user is not following and includes:

Icon

Username with link to /u/&lt;user_url_slug/

<h4>/p/&lt;postid_url_slug&gt;/</h4>

<a href="https://eecs485staff.github.io/p1-insta485-static/images/screenshot-p-1.png">screenshot 1</a>, <a href="https://eecs485staff.github.io/p1-insta485-static/images/screenshot-p-2.png">screenshot 2</a>, <a href="https://eecs485staff.github.io/p1-insta485-static/images/screenshot-p-3.png">screenshot 3</a>, <a href="https://eecs485staff.github.io/p1-insta485-static/images/screenshot-p-4.png">screenshot 4</a>

This page shows one post. Include the same information for this one post as is shown on the main page <sub>/ </sub>.

<h2>Test</h2>

Run the public autograder testcases on your <sub>insta485 </sub>.

$ pytest tests/test_followers.py tests/test_following.py tests/test_generated_html.py test

<em>… </em>

========================== 17 passed in 5.59 seconds ===========================

<h2>Error messages</h2>

Catch all jinja, json, and FilenotFound exceptions and print sensible error messages (make sure the error message starts with ‘Error_’). Then, exit non-zero. Here’s an example:

$ pwd/

/Users/awdeorio/src/eecs485/p1-insta485-static

$ insta485generator insta485

Error_JSON: failed to parse insta485/config.json Expecting value: line 370 column 1 (char 8976)

$ echo $?

1

Make sure the errors begin as described:

For all <sub>jinja</sub> related exceptions, the error begins with Error_Jinja For all <sub>json</sub> related exceptions, the error begins with Error_JSON

For all <sub>FileNotFound</sub> related exceptions, the error begins with Error_FileNotFound

Note: in the bash shell, <sub>echo $?</sub> prints the exit code (return value) of the previous command.

You should handle the case in which the output directory already has files in it. The example below shows how the program should behave in this case.

$ rm -rf hello/html

$ insta485generator hello

$ insta485generator hello

Error_Output_Dir: output directory already contains files: hello/html

<h1>Submitting and grading</h1>

Run the published autograder test cases locally.

$ pytest tests/

<em>… </em>

========================== 38 passed in 12.67 seconds ==========================

Submit a tarball to the autograder, which is linked from <a href="https://eecs485.org/">https://eecs485.org</a><a href="https://eecs485.org/">.</a> Include the <sub>–</sub>disable-copyfile flag only on macOS.

$ tar 

–disable-copyfile 

–exclude ‘*__pycache__*’ 

–exclude ‘insta485/html’ 

-czvf submit.tar.gz 

bin    html    insta485    insta485generator    setup.py

The autograder will run <sub>pip install -e YOUR_SOLUTION </sub>. The exact library versions in the setup.py provided with the starter files is cached on the autograder, so be sure not to add extra

library dependencies to <sub>setup.py </sub>.

Avoid adding any large images to the tarball. The Autograder may throw an error in case the size of the tarball is greater than 5MB. Use the following command to verify the size of the tarball:

$ du -h submit.tar.gz

2.1M    submit.tar.gz

Direct link to the Fall 2019 Project 1 autograder: <a href="https://autograder.io/web/project/404">https://autograder.io/web/project/404</a>.

<h2>Rubric</h2>

This is an approximate rubric. Note than we cannot give additional information about what the private testcases do. To maximize points, make sure that you are following all directions in the spec. Note that the public tests cases do not test everything that your program must do.

<table width="372">

 <tbody>

  <tr>

   <td width="305"><strong>Test</strong></td>

   <td width="67"><strong>Value</strong></td>

  </tr>

  <tr>

   <td width="305">Public unit tests</td>

   <td width="67">50%</td>

  </tr>

  <tr>

   <td width="305">Public Python and HTML style</td>

   <td width="67">10%</td>

  </tr>

  <tr>

   <td width="305">Hidden unit tests run after the deadline</td>

   <td width="67">40%</td>

  </tr>

 </tbody>

</table>

<h1>FAQ</h1>

<strong>Can I use Python2?</strong>

No. You can check your version of your default Python like this:

$ python –version Python 2.7.13

After activating a virtual environment, the default <sub>python</sub> executable may change. For example:

$ python3 -m venv env

$ source env/bin/activate

$ python –version Python 3.6.1

<strong>Can I disable any code style checks?</strong>

Do not disable any code style check from any code style tool ( <sub>pycodestyle </sub>, <sub>pydocstyle </sub>, pylint ).

<strong>Can I spawn new processes?</strong>

When writing <sub>insta485generator </sub>, do not use any code that spawns a new process. The autograder will fail if new processes are spawned. Examples of Python snippets that spawn a new process: os.system() , sh.ls() , subprocess.check_call() . If you’re uncertain whether a new process is being spawned, please ask!


