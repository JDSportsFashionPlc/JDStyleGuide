JD Sports Fashion plc
==================

# Front-End Coding Guide (not official yet)

JD Sports Fashion plc is one of the worlds leading sports fashion retail conglomerates. We have over 35 companies in over 200 countries and have platforms for all brands on mobile, desktop and tablet. This also includes store kiosks and other channels including social and third party vendor sites such as Amazon, eBay and much more. We have a range of platforms from IBM WebSphere Commerce to Magento to Aurora to MESH to Oracle ATG Oracle Retail to IBM DB2 and more.. custom feed driven platforms, custom in-house platforms including custom architecture.. chuck in the fact that we are multi language, multi currency, multi device, multi platform, multi facia and we have multi development teams (globally).. therefore it is imperative that we stick and try to have a consistant codebase across our group.

# Welcome to JD.

---------------------------------------------------------------------------------------------------

### <a name='contents'>Contents</a>

#### [General](#general)
1. [Comments](#code-comments)
1. [Indenting](#general-indenting)
1. [Capitalisation](#general-capitalisation)
1. [Spacing](#general-spacing)
1. [Encoding](#general-encoding)
1. [Minification](#minification)

#### [Architecture](#arc)
1. [Name Conventions](#arc-namc)
1. [Folder Structures](#arc-fold)
1. [Live/Staging File Names](#arc-file)

#### [HTML](#html)
1. [General](#html-general)
1. [Semantics](#html-semantics)
1. [Style](#html-style)
1. [Formatting](#html-formatting)

#### [CSS](#css)
1. [Style](#css-style)
1. [Formatting](#css-formatting)

#### [JavaScript](#javascript)
1. [Writing](#javascript-writing)
1. [Libraries/Frameworks](#javascript-frame)

#### [Info](#info)

---------------------------------------------------------------------------------------------------

## <a name="general">General</a>

### <a name="code-comments">Indenting</a>

Every line of code, every snippet, every service layer requires the global JD comment wrapper. You can do this block for html with `<!--` and for any other language as needed. The block contains your name, the date, and also the hashtag of the campaign. So for example all code, libraries and other files you work contains will have this block.
    
    
    /***
	* --- --- --- --- ---
	* JD Sports Fashion plc
	* IBM WebSphere Commerce Platform
	* Khaleel Mughal - 15.12.2014
	* --- --- --- --- ---
	* #JDFRONTENDSPEC
	* --- --- --- --- ---
	***/
	
	
Generally speaking all code commenting should be used via // and then good annotation of the block in question
    
    BAD JavaScript Comments
    // fix for fmd
	 var f=3;
    
    
    GOOD JavaScript Comments
    // VARS
    // -- Fixes .fmd classes in bootstrap
	 var strFMDInjectionFix = 3;
	 
	 
### <a name="general-indenting">Indenting</a>

Use two spaces to indent. Two spaces is enough space to illustrate heirarchy, but not so much that deeply nested HTML gets out of hand.

Don't use tabs or mix tabs and spaces. Tabs can vary in width for different editors and look especially bad when viewing source-code in the browser.
    
    <ul>
      <li>Felix</li>
      <li>Simba</li>
    </ul>
    
    
    .breeds {
      background: #000000;
      color: #0000FF;
    }

    var purr = function() {
      alert('purr');
    }
    

### <a name="general-capitalisation">Capitalisation</a>

Use only lowercase for all HTML and CSS code. This applies to HTML element names, attributes, attribute values (unless text/CDATA), CSS selectors, properties, and property values (with the exception of strings).
	
    <!-- bad -->
    <A HREF="http://google.com" title="GREAT search engine">Google</A>

    <!-- good -->
    <a href="http://google.com" title="GREAT search engine">Google</a>
    
    <!-- bad -->
    <h1 class="LOGO">I Love Cats</h1>

    <!-- good -->
    <h1 class="logo">I Love Cats</h1>
    

### <a name="general-spacing">Spacing</a>

Remove trailing whitespaces, they can complicate diffs.

### <a name="general-encoding">Encoding</a>

Use UTF-8

Specify the encoding in HTML templates and documents via `<meta charset="utf-8">`. Do not specify the encoding of style sheets as these assume UTF-8.

**[[⬆]](#contents)**

---------------------------------------------------------------------------------------------------

## <a name="html">HTML</a>

### <a name="html-general">General</a>

Use HTML5: `<!DOCTYPE html>`

Use valid HTML where possible.

Use tools such as the [W3C HTML validator](http://validator.w3.org/nu/) to test.

### <a name="html-semantics">Semantics</a>

Use elements for what they have been created for. Using HTML according to its purpose is important for accessibility, reuse, and code efficiency reasons.  

    <!-- bad -->
    <div class="header">
      <div class="title">Cat Massage 101</div>
      <div class="subtitle">Keeping your cat happy</div>
    </div>

    <!-- good -->
    <header>
      <h1>Cat Massage 101</h1>
      <h2>Keeping your cat happy</h2>
    </header>
    

For more information on the specifics of HTML5 elements, see <http://diveintohtml5.info/semantics.html#new-elements>

### <a name="html-style">Style</a>
#### Entities

Use entity references like `&pound;`, `&euro;`, `&mdash;`, `&rdquo;`, or `&#x263a;`, as we cannot assume the same encoding (UTF-8) is used for files and editors.

    <!-- good -->
    <p>OMG I &hearts; &hearts; &hearts; CATS</p>

    <!-- bad -->
    <p>OMG I ♥ ♥ ♥ CATS</p>
	 
#### Type attributes

Omit `type` attributes for style sheets and scripts.

Specifying type attributes in these contexts is not necessary as HTML5 implies text/css and text/javascript as defaults. This can be safely done even for older browsers.

    <!-- bad -->
    <link rel="stylesheet" href="style.css" type="text/css">
	<script type="text/javascript" charset="utf-8"></script>

    <!-- good -->
    <link rel="stylesheet" href="style.css">
	<script>
    

### <a name="html-formatting">Formatting</a>

#### General

Use a new line for every block-level element, and indent child elements.

    <!-- bad -->
    <header><h1 class="logo"><a href="/">CATSRUS</a></h1></header>

    <!-- good -->
    <header>
      <h1 class="logo"><a href="/">CATSRUS</a></h1>
    </header>
    

If you run into issues around whitespace between list items it’s acceptable to put all li elements in one line.

    <!-- ok -->
    <nav>
      <ul>
        <li><a href="/item-1">Item 1</a></li><li><a href="/item-2">Item 2</a></li><li><a href="/item-3">Item 3</a></li>
      </ul>
    </nav>
    
    <!-- preferred -->
    <style>
      nav { font-size: 12px; }
      nav ul { font-size: 0; } /* set font size to '0' to collapse white-space */
      nav ul li { font-size: 12px; } /* reset font size */
    </style>

    <nav>
      <ul>
        <li><a href="/item-1">Item 1</a></li>
        <li><a href="/item-2">Item 2</a></li>
        <li><a href="/item-3">Item 3</a></li>
      </ul>
    </nav>
    

#### Quote marks

Use double (`"`) rather than single (`'`) quote marks around attribute values.

    html
    <!-- bad -->
    <a href='/favourite-kittens'>Favourite Kittens</a>

    <!-- good -->
    <a href="/favourite-kittens">Favourite Kittens</a>
    
    
**[[⬆]](#contents)**

---------------------------------------------------------------------------------------------------
 
## <a name="arc">Architecture</a>

### <a name="arc-namc">Name Conventions</a>

Use camel casing; THISISNOTPOOR compared to camelCasing.
Use full British English.
Do not use slang or name initials; full names, dates and full language.
Do not use any profanity and keep it logical and comments most be purposeful.
Use generic names and do not spam text for SEO.
Use good names for images for better searching.

### <a name="arc-fold">Folder Structures</a>

	GOOD
	/page/news
	/page/news/sports
	/page/news/sports/302242-David-Beckham-joins-JD-Sports
	
	FILE PATHS
	/lib/www/apps/news/
	/lib/www/apps/news/sports
	/lib/www/apps/news/sports/302242.htm
	
	DB
	/lib/www/apps/news/articleViewer.jsp?articleId=302242
	
	IMAGES AND MEDIA
	/assets/media/css/main.css
	/assets/media/css/product.css
	/assets/media/imgs/brands/adidas.jpg
	/assets/media/imgs/jd/jd-sports-logo.jpg

	
### <a name="arc-file">Live/Staging File Names</a>	
Look at this folder. The src files are code commented. And minified files are for distribution.
 
    GOOD
    /page/nike/
    /page/nike/index.src.html
    /page/nike/index.html
 
    GOOD
    /page/nike/
    /page/nike/index.dev.html
    /page/nike/index.html
 
    GOOD
    /page/nike/
    /page/nike/js/dev.js
    /page/nike/js/dev.packed.js
 
    GOOD
    /page/nike/
    /page/nike/css/framework.css
    /page/nike/css/framework.min.css
 
 
Always have a .compress, .src or .dist file alternative of your minified file - minified files should be served first. Use GruntJS or any other tool which does good compression without breaking and destroying your JS or CSS.

**[[⬆]](#contents)**

---------------------------------------------------------------------------------------------------
 
## <a name="css">CSS</a>

### <a name="css-general">General</a>

Use valid CSS

Use tools such as the [W3C CSS validator](http://jigsaw.w3.org/css-validator/) to test.

### <a name="css-style">Style</a>

#### Naming
 
Prefer classes to IDs, classes are reuseable and do not interrupt CSS hierarchy. A good rule of thumb is to *ONLY* use an ID when you need to do something with the element in JavaScript. Styles should almost always be aplpied with a class.

Use meaningful or generic names for IDs and classes. Do not use camelcase CSS names. All CSS should be lowercase and separated with a hyphen.

    /* bad */
    .a {}
    .kjs-0922 {}

    /* good */
    .video {}
    .street-address {}
    

Use names that are as short as possible but as long as necessary.

    /* bad */
    .navigation {}
    .atr {}

    /* good */
    .nav {}
    .author {}
    

Separate words in IDs and class names with a hyphen and use only lowercase characters

    /* bad */
    .CHUBBY-CATS {}
    .crazyCats {}
    .cranky_cats {}
    .creepycats {}

    /* good */
    .cute-cats {}
    

#### Type selectors

Avoid specifying unecessary type selectors or ancestors

    /* bad */
    ul.cats {}
    header.main h1.logo span {}

    /* good */
    .cats-list {}
    .logo span {}
   

If coding in LESS, avoid Christmas trees by nesting everything. Three levels deep should be plenty.

#### Shorthand properties

Use them

    /* bad */
    li {
      border-top-style: none;
      font-family: palatino, georgia, serif;
      font-size: 100%;
      line-height: 1.6;
      padding-bottom: 2em;
      padding-left: 1em;
      padding-right: 1em;
      padding-top: 0;
    }

    /* good */
    li {
      border-top: 0;
      font: 100%/1.6 palatino, georgia, serif;
      padding: 0 1em 2em;
    }
    

#### Zeros

Don't include units after `0` values unless they are required

    /* bad */
    li {
      margin: 0em;
      padding: 0%;
    }

    /* good */
    li {
      margin: 0;
      padding: 0;
    }
    

Don't include a leading `0` in values between `-1` and `1`

    /* bad */
    li { font-size: 0.8em; }

    /* good */
    li { font-size: .8em; }
    

#### Colours

Use hexadecimal notation

    /* bad */
    a { color: rgb(0,0,255); }

    /* good */
    a { color: #0000FF; }
    

Prefer three character hexadecimal notation where possible

    /* bad */
    p { color: #000000; }

    /* good */
    p { color: #000; }
    

#### Hacks

Avoid user agent detection as well as CSS "hacks" - try a different approach first.

One exception to this is the "clearfix" hack to force an element to clear it's children. For support in IE8 and up this one is fairly efficient:

    .group:after {
      content: "";
      display: table;
      clear: both;
    }
    

### <a name="css-formatting">Formatting</a>

#### Declaration order

Alphabetise declarations.

Put declarations in alphabetical order in order to achieve consistent code in a way that is easy to remember and maintain.

Ignore vendor-specific prefixes for sorting purposes. However, multiple vendor-specific prefixes for a certain CSS property should be kept sorted (e.g. -moz prefix comes before -webkit).

    css
    .main-header {
      background: #000;
      border: #FFF solid 4px;
      border-radius: 4px;
      -moz-border-radius: 4px;
      -webkit-border-radius: 4px;
      color: #FFF;
      text-align: center;
    }
    

#### Declaration order
Indent all block content

    /* bad */
    @media screen, projection {

     html {
     background: #fff;
     color: #444;
    }
    }

    /* good */
    @media screen, projection {

      html {
        background: #fff;
        color: #444;
      }
    }

#### Declaration stops
Use a semicolon after every declaration

    
    /* bad */
    li {
      margin: 0;
      padding: 0
    }

    a { color: #FF0000 }

    /* good */
    li {
      margin: 0;
      padding: 0;
    }

    a { color: #FF0000; }
    

#### Spacing
Use no single space between property and value (and no space between property and colon). There should be no trailing final ;} too. See minification above too

    /* bad */
    h1 { font-weight:bold; }
    h1 { font-weight :bold; }

    /* good */
    h1{font-weight:bold}
    
Use no single space between the last selector and the opening brace that begins the declaration block.  
The opening brace should be on the same line as the last selector in a given rule.

 
    /* bad */
    .video{
      margin-top: 1em;
    }

    .video
    {
      margin-top: 1em;
    }

    /* good */
    .video{margin-top:1em}


You may start a new line for each selector and declaration.

    /* bad */
    input:focus, input:hover {
      background: #FFFF00;
    }

    /* good */
    input:focus,
    input:hover {
      background: #FFFF00;
    }
	 
	 /* also good */
	 input:focus,input:hover{background:#FFFF00;}
	 

No blank line (two line breaks) between rules.

    
    html{background:#fff;color:#000}
    body{margin:auto;width:50%}
    

If you are only declaring one style, write the entire declaration on one line.

    /* bad */
    a {
      color: #ffffff;
    }

    /* good */
    a{color:#fff}
    

Use single `'` rather than double `"` quotation marks for attribute selectors or property values. Do not use quotation marks in URI values `url()`.

    css
    /* bad */
    @import url("//www.google.com/css/maia.css");

    html {
      font-family: "open sans", arial, sans-serif;
    }

    /* good */
    @import url(//www.google.com/css/maia.css);
    html{font-family: 'open sans', arial, sans-serif}
    

**[[⬆]](#contents)**

---------------------------------------------------------------------------------------------------


## <a name="javascript">JavaScript</a>

### <a name="javascript-writing">General</a>

Use the global JD CDN for using the same libraries.

Avoid using Public CDN APIs such as Google.

Do not use execessive whitespace.

Check jQuery for conflicts.

Use camel case in functions.

   
    /* bad */
    function FOOBAR() {}

    /* good */
    function fooBar() {}
    

Use console for testing.

    /* bad */
    alert('test');

    /* good */
    console.log('test');
    
    
 Use JSON Lints for JSON validation - avoid big empty nests.

    
    /* bad */
    page { pages { pagelist { page1 {} page2{} } } } }

    /* good */
	{
	"Page": [
	{
	"Enabled": true,
	"NavHTML": [
			{
				"id": 0,
				"link": "/page/king-of-trainers/",
				"pic": "/lib/hlight/king-of-trainers/assets/images/nav/kot.png",
				"tag": "KOT-_-Navigation-_-Home",
				"text": "King of Trainers - Home",
				"class":"kotNavLogo"
			},
			{
					"id":1,
					"link": "/page/king-of-trainers/",
					"pic": "/lib/hlight/king-of-trainers/assets/images/nav/latest.png",
					"tag": "KOT-_-Navigation-_-Latest",
					"text": "King of Trainers - Latest",
					"class":"link",
					"activeclass":"kotnav-latest"
			},
			{
					"id":3,
					"link": "/page/king-of-trainers_mission-statement/",
					"pic": "/lib/hlight/king-of-trainers/assets/images/nav/mission.png",
					"tag": "KOT-_-Navigation-_-Mission",
					"text": "King of Trainers - Mission Statement",
					"class":"link",
					"activeclass":"kotnav-missionstatement"
			}
			]
		}
	]
	}
    
    
Use good cloaking when using Angular.

ALWAYS serve JS through defer and at the footer of the HTML document
 
 
### <a name="javascript-writing">Frameworks and Libraries</a>

Use the global JD CDN for using the same libraries.

Try to use Amazon CDN or the Akamai buckets for CDN calls; if the library or plugin is out of date, clone the repo and save as .src.backup and apply the same dist and source release updates for making it public - remember to comment and documentate and hashtag the file so it can be updated later

Turn off and remove libraries after you upgrade and delete the folders after about a month to ensure to old callbacks - Use JSLint and jsFiddle for testing.

**[[⬆]](#contents)**

---------------------------------------------------------------------------------------------------


## <a name="info">Info</a>


With help/inspiration from:

- Rob Flynn - JD
- James Holt - JD
- Timi Abel - JD
- Richard Holding - JD
- Adnan Baig - JD
- Przemek Lewtak - JD
- [Gov.UK](https://github.com/alphagov)
- [van der Ende](http://van-der-en.de)
- [Google HTML/CSS Style Guide](http://google-styleguide.googlecode.com/svn/trunk/htmlcssguide.xml)
