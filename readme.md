
* IMPORTANT NOTE: When poushing to github from protected environments or where they use self signer certificates
use: `git config http.sslVerify false` to your repo to be able to push remote (NOT SECURE - NOT FOR IMPORTANT PROJECTSs)

# Section 2 - Natours Project - Setup and First Steps

## Lecture 5 - Project Overview

* Landing Page for a ficional company offering tours in nature
* animations, animated cards, modern flat design. Popups, video in background
* form with modern look and feel
* custom radio buttons
* materialize css style navigation, custom made
* Boilerplate project by tutor. images , css and html boilerplate
* in html file (html5 style) he has already imported:
	* stylesheet
	* favicon : `<link rel="shortcut icon" type="image/filetype" href="path">
	* title
	* googlefont(Lato)
* stylesheet cotnains only color codes

## Lecture 6 - Building the Header - Pt.1

* Lecture objectives: best way to perform basic reset with universal selector, set project-wide font definitions, clip parts of elements using clip-path
* in the past we used normilize.css to reset all browser differences and start from common ground. browsers have normilized in the recent years so its no longer needed. we need to add a gobal reset with the * selector in css setting margin and padding to 0 and box-sizing to border-box. this doesnt add up padding and border to the element height and width we specify allowing easier alignment.
* we use css inheritance (css properties are inherited by child html elements) to add project specific properties. we use selector body to set font-family, fon-size, font-weight, color, and line-height. the font size attribute will be set as reference for later definitions. line height 1.7 is quite high (1.5 is recommended)
* we set header styles using class selector. for height we use 95vh so 95% of veiw height (screen viewport height)
* we set a background image passing its url as background-mage: url(relative path to image)
* we set background-size to cover to stretch the image to fit the viewport (no crop)
* we set backrund-position to top to anchor the image to the top and crop the bottom
* we want a gradient overlay on image. we do so adding one more value to background-image attribute
* the second value is put first (on top) and its syntax is `linear-gradient(to right bottom, #7ed56f, #28b485)` this sets direction to bottom right and start color and end color. as color valus are rgb the opacity is 1 (no transparency). to add transparency we use the rgba values of the colors adding an opacity value (e.g 0.8). the linera-gradient is set before the url separated with a comma
* we want to add to our webpage a photo frame look and feel. we can do so adding a thick padding (e.g 30px) at the body selector wraping all content.
* we dont have to worry about padding inheritance. there are certain css atributes that get inherited
* we want to clip the bottom part of our image. we use modern css property clip-path. in this we specify the polygon where the image will still be visible `clip-path: polygon(0 0, 100% 0, 100% 80%, 0 100%);`
* polygon gets a number of x y coordinates as params which are the points. the coordinates can be absolute pixels or relative to element height and width (%) or vh (100 of viewport height)

## Lecture 7 - Building the Header - Pt.2

* Lecture objectives: center anything with the transform, top and left properties
* we add a div in header to host our logo and our logo as an img with class logo.
* we use absolute positioning for logo-box. putting top and left distance. to use absolute positioning the parend element (header) needs to have relative positioning
* for image we set the height. width is auto set by browser keeping the image aspect ratio
* we add h1 fror title. h1 is very important as it is used by google search engine. we need to make it descriptive so we put subtitle as well and add span for styling.
* we will style two spans (main and sub) as block elements `display: block;`. as this adds linebreaks
* we need to center the heading no matter the resize. and also the button beneath it (TBD). so we add a div box for positioning. to center it we use again absolute positioning given the parent element uses relative. the attributes we set are: 

```
	position: absolute;
	top: 50%;
	left: 50%;
	transform: translate(-50%, -50%);
```

* transform translate is used to subtract the elements dimensions to achieve true center. transform is related to the transformd element.
* top and left are related to the parent element

## Lecture 8 - Creating Coll CSS Animations

* Lecture objective: learn to create CSS animations using @keyframes and animation property
* we want to achieve a fade in entrance from right and left for title and subtitle. we can use transition for opacity or other basic styling but we use @keyframes
* @keyframes aer used for reusable animations that we can add to our elements their syntax is like:

```
@keyframes moveInLeft {
	0% {
		opacity: 0;
		transform: translateX(-100px);
	}

	80% {
		transform: translateX(10px);
	}

	100% {
		opacity: 1;
		transform: translate(0);
	}
}
```

* we use @keyframe name to name it. we set various timing points in animation setting the transformations. in transform we can stack more transformations like rotate translate, translateX (move horizontal). we can specify as many points we want.
* we add the animation to our elements with:

```
	animation-name: moveInLeft;
	animation-duration: 1s;
	animation-timing-function: ease-out;
	/*animation-iteration-count: 3;*/
	/*animation-delay: 3s;*/
```

* τhe first two are required the rest are optional. we can add them in one liner like `animation: moveInRight 1s ease-out;`
* we can add animation in element.states like .button:hover to create cool effects

## Lecture 9 - Building a complex Animated Button - Pt.1

* Lecture objectives: learn what pseudo-elements and pseydo-classes are. how and why to use the ::after pseudoelement. how to create hover animation effect using *transition* property
* pseudoclasses are defined with : we usit to specify further an element like the link states (active: click, hover: mouseover, visited, link: initial state)
* we add box shadow to create distance. `box-shadow: 0 5px 10px rgba(0,0,0,.2);` first param is offsetX, second offsetY, third blur, forth color
* we change the box shadow and we add transformy together to create a press down effect. we make it smooth with transition. `transition: all .2s;` we apply it to all changing properties.
* we make the btn class (link) inline-block to add new line but style it as text. therefore in the parent element we can use text-align: center to center it in the x axis.

## Lecture 10 - Building a complex Animated Button - Pt.1

* we want to add a second animation to the button . like an echo to infinity when we hover
* we use pseudoelement :: to style certain part of an element, e.g ::after creates a virtual element after the element it applies to. this pseudoelement is treated as a child element and can be styled separately. to place it behind  we make the original elements position relative and the pseudoelemenmts position absolute with top and left to 0. to put it behind we use `z-index: -1`.
* to make it expand on certain states we use

```
.btn:hover::after {
	transform: scaleX(1.4) scaleY(1.6);
	opacity: 0;
}
```

* pseudoelement can stack after pesudoclass of parentelement. we make the animation smooth with `transition: all 0.4s`
* we fade in the button with delay in animation and preventing the initial appearnce of element

```
.btn-animated {
	animation: moveInBottom 1s ease-out .75s;
	animation-fill-mode: backwards;
}
```
* we prevent the initial appearance with `animation-fill-mode: backwards;`

# Section 3 - How CSS Works: A Look Behind the Scenes

## Lecture 12 - Three Pillars of writing good CSS and HTML

* Responsive Design: Fluid Layouts,Media Queries, Responsive Images, Corrent Units, Desktop-first or Mobile-First 
* Maintainable/Scalable Code: Clean,Easy to understand, Growth, Reusable, How to organize files, How to name classes, how to structure HTML
* Web Performance: Less HTTP requests, less code, compress code, use css preprocessor,less images, compress images

## Lecture 13 - How CSS works behind the Scenes: An Overview

* Browser Render Flow: 
	* Load HTML -> Parse HTML-> DOM ->
	* Load CSS-> Parse CSS (Resolve conficts, process final values) -> CSSOM ->
	* -> Render Tree -> visual formating model -> Final Render

## Lecture 14 - How CSS is Parsed, Part1: The cascade and Specificity

*  A CSS rule is composed by *selector* `.my-class` and a *declaration block* `{color: blue;}` a *declaration* `color: blue;` is composed by a *property* `color:` and *declared value* `blue;`
* The *cascade* is the process of combining different stylesheets and resolving conflicts between different CSS rules and declarations, when more than one rule applies to a certain element.
* the cascade resolves issues witht he following criteria: **importance(weight)** > **specificity** > **source order**
	* Order of **Importance**: 1) User *!importance* declarations 2) Author *!important* declarations 3) Author declarations 4) User declarations 5) Default browser declarations  (e.g. `color: blue !important;`)
	* **Specificity** order: 1) Inline Styles 2) IDs 3) Classes, pseudo-classes, attributes 4) elements, pseudo-elements. Selector specificity gets a score (Inline occurences,IDs occurences,Classes Occurences, Elements occurences) e.g `.btn {}` => (0,0,1,0). To check order we check numbers from left to right.
	* The last declaration in code wins.
* `!important` is a no-no same as code order
* the universal selector `*` has NO specificity (0,0,0,0)
* BE CAREFUL when importing 3rd party CSS. ALWAYS put our own stylesheet last to not have problems with order.

## Lecture 15 - Specificity In Practice

* pseudoclass counts as a class in specificity but not as an element...

## Lecture 16 - How CSS is Parsed, Part2: Value Processing

* it is done in 6 stages 1. Declared Value:*author declarations* 2. Cascaded value:*after the cascade* 3. Specified Value: *deafulting if there is no cascade value* 4. Computed Value: *converting relative values to absolute* 5. Used Value: *final calculations based on layout* 6. Actual Value *browser and device restrictions*
* Browser Default values are added as Stage2
* Inherited values are added at Stage 3.
* Missing value initializations at Stage3
* calculated values based on parent value at stage 4
* subpixel roudup at stage 6.
* % in fonts: converted to x% * parents computed font-size
* % in lengths: converted to x% * parenets computed **width**
* em in fonts: converted to x * parent computed font-size
* em in lengths: converted to x * **current**element computed font-size
* rem: converted to x * root computed font-size
* vh: convert to x * 1% of viewport height
* vw: convert to x * 1% of viewport width

## Lecture 17 - How CSS is Parsed, Part3: Inheritance

* a way of propagating properties from parent to child
* it is used if there is no cascaded value and if the property can be inherited
* inherited percentages are calculated based ont he parents base value to of the child
* if there is no inherited value we get the initial value
* properties related to text **are** inherited
* properties related to box or dimencions are **not** inherited
* the *inherit* property forces inheritance to a property , *initial* resets it to initial value

## Lecture 18 - Converting px to rem: An effective workflow

* Lecture objectives: how and why use rem units in our project, a good workflow to convert px to rem
* good practice for responsive media queries
* Workflow: first we define a font-size at html level `html {font-size: 10px}`. we use 10px to make calculations easy (divide by 10)
* we replace ALL px  values to rem (takes value from html root tag)
* we just change root font size to see the
* by specifing the font-size at html level we remove the ability of a user to change the browser font size manualy. we dont want that. so we specify as apercetage of teh browser default gont size which is 16px. the rule becomes `html {font-size: 62.5% }`
* we use inherit to make box-sizing property inheritable at global level and we define it at body level. (good practice)
* an other good practice is to define the global rule as `*,*::before,*::after {}` to apply at the pseudoclasses we might use

## Lecture 19 - How CSS Renders a Website: The Visual Formatting Model

* VFM definition: *Algorithm that calculates boxes and determines the layout of these boxes, for each element in the render tree, in order to determine the final layout of the page*
* VFM takes into account: Dimensions of boxes, Box Types, Positioning Scheme,Stacking Contexs, elements in rendr tree, viewport size imaged dimentsions etc.
* The box model is fundamental content is surrounded by padding which is surreounded by border which is surrounded by margin. the fill area that gets the background is content+ padding+ border
	** Box model total width = right border + right padding + width + left padding + left border
	** box model total height = top border + top padding + height + bottom padding + bottom border
	** `box-sizing: border-box;` makes life simpler with less calculations as height = total height and width = total width 
* Box Types:
	** Block-level boxes: elements formatted visually as blocks, 100% of parents width, vertically one after the other, box model applies. they are declared as `display: block` or *flex* or *list-item* or *table*
	** Inline boxes:  content is distributed in lines, ocupies only contejnt space, no line breaks, no heights and widths only horizontal paddings and margins (left right) `display: inline`
	** Inline-block boxes: a mix of block and inline, occupies only contents space, no line braks, box model applies `display: inline-block`
* Positioning Schemes: 
	* Normal FLow: default positioning scheme, not floated, not absolute positioned, eleemts laid out according to their source order `position: relative`
	* FLoats: element is removed from normal flow, text and inline elements will wrap around the floated element, the container will **not** adjust its height tot he element . it is moved as far as posible to the parent componetns limits` float: right float: left`
	* Absolute positioning: element removed from normal flow, no impact on surrounding content (can overlap them), we use top, left, right, bottom to offset it from its relative postiioned container `position: absolute` `postion: fixed
* Stacking context: is the z-index the z axis stack. `z-index: -1` the higher index appears on top

## Lecture 20 - CSS Architecture Components and BEM

* **Think** about the layout of yur webpage or webapp before writying code
* **Build** the layout in HTML and CSS with constant structure in naming classes
* Create a logical **architecture** for your CSS with files and folders
* Think: Component Driven Design: create modular building blocks that make interfaces, held together by layout of page, re-usable across a project and between projects. Follows principle of Atomic Design
* Build: Block Element Modifier (BEM): `.block {} .block__element {} .block__element--modifier {}
	* BLOCK standalone component is meaningful on its own
	* ELEMENT part of teh block tht has no meaning on its own
	* MODIFIER a different version of a block or an element
* Architect: 7-1 pattenn. & different folders for partial sass files , 1  main folder to import all other files into a compiled CSS stylsheet.
* 7 folders (base/ components/ layout/ pages/ themes/ abstracts/ vendors/)

## Lecture 21 - Implementing BEMs into Natours project

* header is a block. logo-box is an element (has no meaning without the header) heading-primary is a block main is amodifier

# Section 3 Intro to SASS and NPM

## Lecture 23 - What is SASS?

* SASS is CSS Preprocessor that adds power and elegance to the language
* SASS Source ->Sass Compiler-> CSS Compiled Code
* SASS gives us:
	* **Variables** : for reusable values like corors, font-sizes, spacing etc
	* **Nesting** : to nest selectors inside of one another allowing us to write less code
	* **Operators : for mathematical operations right inside CSS
	* **Partials and imports** : to write CSS in differenet files and import thme all in a single file
	* **Mixins** : to write reusable pieces of CSS code
	* **Functions** : similar to mixins, with the difference that they produce a valu that can be used
	* **Extends** : to make different selectors inherit declarations that are common to all of them
	* **Control Directives** : for writing complex code using conditionals and loops (not covered in the course)
* SASS syntax:

```
.navigation
	list-style: none
	float: left
& li
	display: inline-block
	margin-left: 30px
```

* SCSS syntax:

```
.navigation {
	list-style: none;
	float: left;

	& li {
		display: inline-block;
		margin-left: 30px;
	}
}
```

## Lecture 24 - First Steps with SASS: Variables and Nesting

* variables are deifned with $ *$variablename: variablevalue;* eg. `$color-text: #f2f2f2;` they are reusable and be placed in rules instead of the value e.g `color: $color-text;
* Nesting is done instead of cascading selectiors e.g. `nav ul li {color: white;}` is equivalent to 

```
nav {
	ul {
		li {
			color: white;
		}
	}
}
```

* pseudoclasses can be nested by using the & symbol eg. `nav li::first {color: white;}` is equivalent to 

```
nav {
	li {
		&::first {
			color: white;
		}
	}
}
```

* if we set all elements in the save level with float: the parrent becomes inline collapses and loses its height (and background). to fix this we do the clear fix.
in the parent element we add clearfix class which we syle as :

```
.clearfix::after {
	conten: "";
	clear: both;
	display: table;
}
```

## Lecture 25 - First Steps with SASS: Mixins Extends and Functions

* mixin are reusable multiline object type set of properties that can be included in rules. they are  defined by the @mixin infront the mixinname and are called with @include mixinname e.g:

```
@mixin clearfix {
	&::after {
		conten: "";
		clear: both;
		display: table;
	}
}

nav {
	@include clearfix;
}
```

* mixins can be parametrical. they can take variables as inputs like functions e.g.

```
@mixin style-link-text($color) {
	text-decoration: none;
	color: $color;
}

.link-1 {
	@include style-link-text(#fff);
}

.link-2 {
	@include style-link-text($color-dark);
}

* some functions are icluded in sass like `color: ligthen($color-dark,10%);`
* they take some arguments do something with them and return a value
* we can add custom  functions followin a prog . language syntax.

```
@function divide($a, $b) {
	@return $a / $b;
}

div {
	margin: divide(60, 3) * 1px; // = 20px
}

* extends is used to apply dry principle setting in the variable not the properties it includes but the selectors it is applied to. it copies selectors not properties. it is defined with % and is applied with @extend


```
%btn-placeholder {
	padding: 10px;
	display: inline-block;
	text-align: center;
} 

.btn-main {
	&:link {
		@extend %btn-placeholder;
	}
}

.btn-hot {
	&:link {
		@extend %btn-placeholder;
		color: red;
	}
}
```

is translated to :

```
.btn-main:link, .btn-hot:link {
	padding: 10px;
	display: inline-block;
	text-align: center;
} 

.btn-hot:link {
	color: red;
}

```


* we should prefer extend over mixin if the rules are thematicaly related

## Lecture 27 - NPM Packages: Let's Install Packages Locally

* in the project root folder
* `npm init` then `npm install --save-dev node-sass` to install sass compiler as a dev tool. we dont need it in production as it will generate the css file for production. 

## Lecture 28 - NPM Scripts: Let's Write And Compile SASS Locally

* mkdir folder /sass in project . we create main.scss file and paste there all style.css code. css is valid scss.

* we set our colors as variables. we use these variables at rgba value as `rgba($color-primary-light,0.8),` This works only in sass. to set an rbg hex value in rgba.

* we compile by adding a script in package.json sripts object `    "compile:sass":"node-sass sass/main.scss css/style.css"`
* this script takes as input sass/main.scss and compiles it to css/styles.css file.
* the output is linked in the index.html for rendering
* we call the script with npm run compile:sass in the root folder
* we add -w flag int he end of our script to run as deamon and watch for changes

## Lecture 29 - Auto reload page

* we install live-server to reload our page as we save `npm install --g live-server`
* we run it with `live server`

# Section 5 - Natours Project - Using Advanced CSS and SASS (Part 2)

## Lecture 31: Converting our COde to SASS: Vars and Nesting

* we start making all colors into sass variables
* we nest our selectors. as we used BEM for naming and we style with classes there is not much space for nesting
* we use the name interpolation character & we used in pseudoclasses to make nesting possible with classes.

```
.header {
	color: black;
}

.header__logo-box {
	color: red;
}
```

becomes

```
.header {
	color: black;
	&__logo-box {
		color: red;
	}
}
```

## Lecture 32: Implementing the 7-! Architecture with Sass

* 7-1 architecture makes sense i in large multipage projects
* we import the files in our main.scss with `@import "folder/fileName";` without .scss
* We create 7 subfolders in our sass folder 
	* base: contains low level rules (animations,base, tyography,utils) as partials (_filename.scss)
	* abstracts: contains code that is not gonna output any css (variables & mixins etc) as partials.
	* compoents: for our components, reusable blocks that make our website or app
	that need to be independent
	* layouts: here we put project global layout styling (headers, footers and stuff)
	* pages: if he have specific styles for a specific page , we create a file for the specific page with its name (_home.scss)
	* themes: in case we do a webapp with different themes
	* vendor: 3rd party css from e.g bootstrap
* we import all the partials we created in main.scss
* we restart the script compile:sass (it breaks when we create files)
* we cut paste color variables in _variables.scss
* we cut paste our basic selectors (html elements) rulesin _base.scss
* @keyframe animations are cut paste in _animations.scss
* .btn can become a component a building block that we can reuse so we create a file _button.scss in compoennts and cut paste .btn {}
* .header can be used as a layout (global layout) or as a component. we choose to consider it global and create file _header.scss in layouts where we cut paste the rule.
* .heading-primary we consider it typography so we place it in the respective file. it could be used as a component (questionalble)
* we note that in many places we have typography stuff in rules. we should place them in _typography as well

## **IMPORTANT NOTE** In @imports order is very important. import with order of folders and files (alphabeticaly)

## Lecture 33 - Basic Principles of Responsive Design and Layout Types

* Basic Responsive Design Principles
	* Flow Grids and Layouts: To allow content to easily adapt to the current viewport width used to browse the website. uses % rather than px for layout related lengths
	* Flexible/Responsive Images: Images behave differently than text content and so we need to ensure that they also adapt nicely to the current viewport
	* Media Queries: To change styles on certain viewport width (breakpoint). allowing us to create different version of our website for different widths
* Float Layouts are not new. they are globally supported . they do 1 dimension layouts.
* Flex is new and easy for 1d layouts. CSS Grid is new and does 2d layout

## Lecture 34 - Building a Custom Grid with Floats

* Lecture objectives: how to architect and build a simple grid system. how the attribute selector works. how the :not pseudoclass works. how cal() works and whats the difference between calc() and simple Sass operations
* we will buid a maximum 4 column grid.
* columns aligned are always in a container called *.row*
* we write html markup to test our grid style not for production
* to implement our grid we do it in layout in a new _grid.scss file
* we implement the .row rule adding the max-width: propery in rem. we use rem to easily change it with media queries also we use max-width to be able to shrink/adapt in small screens
* we add `margin: 0 auto;` to .row to center it
* we want a distance between rows  so we add `margin-bottom:`
* we put length is _variables
* we dont want the last row to have margin bottom so we use 

```
	&:not(:last-child) {
		margin-bottom: $gutter-vertical;
	}
```

* :not pseudoclasss reverses the pseudoclass wraped so in essence it says apply this rule to all but the wrapped pseudoclass . all except last-child
* we place the column rules in the row rule as it is the logical order in our markup. (there is no sence in a column without row)
* we use the css functiuon calc to calculate the width.`#{$variable}` to work.
* we use not again to apply horizontal gutter and we use float: left to do the fluid layout. as we said before this makes the parent element colapse (the wrapping div) so it loses its height as it becomes inline. so we need the clearfix to solve it. we place it in mixins and we include it in row
* to style columns we use scss atributes. this is a powerful selector that uses html attributes to select elelemnts for styling. its syntax is `[attr="someVal"] {}`, if we use instead of = ^= it means *if attribute val starts with..* $= it means *if attribute val ends with..*. e.g `[class^="col-"]{}`

## Lecture 35 - Building the About Section: Part 1

* Lecture Objectives: Thinking about components, how and why to use classes, how to use the *background-clip* property, how to *transform* multiple properties simultaneously, how to use *outline-offset* property together with *outline*, how to style elements that are NOT hovered while others are.

* we add a new section to our markup: `<main></main>` to telle search engines this is the maain part of our website. header+ main+footer
* he uses emmet (sublime palugin) (yeah right...)
* we add a new section (its styles in _home.scss and a new heading (in _typography.scss)
* we style our section adding a large padding and background color. to eliminate the white triangle header we move up the section by a negative margin (95vh -75vh = 20vh)
* in typography we style secondary heading. a trick to make it a gradient color is shown below

```
	display: inline-block;
	background: linear-gradient(to right, $color-primary-light, $color-primary-dark);
	-webkit-background-clip: text;
	color: transparent;
```

* what we do is we set a background image gradient. we make it the size of text with inline -block, then we use the webit propery background-clip. to clip it around text and then we dissaperear the text to make it appear from behind.
* we add an animation with transform when hovering over. we use skewY to distort on Y axis `transform: skeyY(2deg);` we apply it to the element with `transition: all .2s;`
* with transform we can cascade transformations
* *text-shadow* property is the same with *box-shadow* but for text
* we need to center it. the way to do it is to put it in a parent element and center that
* we will use *utility classes* to do this. utility classes are simple calsses in CSS that have only one goal. in our case is to center the child element
* they are used with reusability in mind and placed in _utilities partial scss file
* we center it with text-align as the heading is styled as inline-block so it is positioned as inline element (text)
* we want to use the grid to position elements so we copy paste blocks from our test markup. styling is already there and tested
* we need spacing after the secondary heading BUT we want it resusable and in other uses the margin requirements are digfferent
* to solve it we use a utility class!
* we add h3 and paragraph and style it with typography and utility classes. we use psedoclasses and elector interpolatiuon with &. nothing new
* we start bulding a new buttona as an anchor. we style in _buttons.
* padding and borders for small buttons is better to be in px not rem.
* we will style images with animations. we create a new component in components _composition and we apply the BEM convention in naming. we use nesting with & to structure rules
* we give them 55% width of the parent element (col)
* we want them on top ofeach other. we use absolute positioning. when we set absolute they take reference with the paret with relative so we make the container relative position. they are stacked in top left corner . all zeroed.
* we position them using the modifier classes.
* TO MAKE IMAGES RESPONSIVE WE SET THEIR WIFDTH IN %!
* we play with the z-index to make an animation efect of changing height
* we want to add a boder at a distance from the element like a frame.

* a trick to scale down siblings when hovering over an element is. beacuse events propagate when we hover a child the parent also gets thge pseudoclass hover. we take advantage to add at parent level (if we use css class nesting)

```
	&:hover &__photo:not(:hover) {
		transform: scale(0.9);
	}
```

* this means if the parent changes state to hover scale down all children (using BEM naming) that they are not hovered .

## Lecture 38 - Building the Features Section

* Leture objectives: Include and use  icon font,creating skewed section design, how and when to use the direct child 
* we download icon fonts from linea.io. we extract fonts folder and styles.css in our css folder. we rename styles to icon-font and include it in our index.html. we get one class for each font
* we use the icon with the i tag `<i class="icon-basic-world"></i>`
* we create boxes for our content. we want to add animation to them. we never do transformations on the grid. we use boxes
* our feature box will be a component so we use BEM
* we style the section in _hove adding padding.
* we insert a background image in section with: 

````````
	background-image: linear-gradient(
		to right bottom, 
		rgba($color-primary-light,0.8), 
		rgba($color-primary-dark,0.8)
	), url(../img/nat-4.jpg);
	background-size: cover;
````````

* we extract as amixin grading linear text implementation from typography ad include it in icons.
* we skew the section in _home but the skew affects also the childs (the boxes). we need to skew the boxes in the oposite direction. we dont do it in the component file because we want themto be reusable. we do it where we do the section skew in _home using the direct child selector *>* and the global selector (all children) ***.

```
	& > * {
		transform: skewY(7deg);
	}
```

* this method does not affect the classes per se but the html elements 

## Lecture 39 - Building the Tours Section: Pt. 1

* Lecture Objectives: build a rotating card, use *perspective* in CSS, use *backface-visibility* property, use background *blend* modes, how and when to use *box-decoration-break*
* we make a new section and style it in _home. we copy paste the h1 block from section-about and copy paste our grid markup for 3 columps. we copy paste padding and background color from section-about and se the mardin to cover white spaces.
* we make new component *card" and add its partial to main.scss
* in the card we add when hovered trransform with rotation on Y axis for 180deg `transform: rotateY(180deg);` . we see that it doesn look right. we need perspective
* perspective is defined on the parent element we want to rotate so we add it to card and the animation to a child ( a div with a BEM compatible element name). the rest of the styling is done in the childe element .card_side.
* we bind the hover rule to the parent aplying it to the child. we could do the following 

```
&__side {
	&:hover {
		transform: rotateY(180deg);
		background-color: $color-primary-light;
	}
}
```

* but we would have to rewrite the rule . with the following selector `&:hover &__side {}` inside the parent we can apply it to more children. the transition is still defined in the element the rule is applied `&__side {}`
* to implement both sides of the rotating card we need 2 divs of card__side withan additional modiffing class *card__side--front* and back. this is to style the 2 sieds of the card.
* the back card__side starts with transform: rotateY(180deg) and transitions to 0deg. we apply the transform on hover on both classes . and we see that they are one below the other. to stack them we use `position: absolute` (this has to do with the element div so we apply it to the common class card__side) and at the parent div (card) position: relative. absolute position makes the size 
* relative to the content (text) so we give width relative to the parent 100%. we see that dimesions are right but on transition one hides the other so we add `backface_visibility: hidden;`
* we see that there is no perspective. this is because parent lost its height. this is because it collapsed due to both children in position absolute. for floats we have clearfix. for this there is no clearfix. we need to five the parent aheight (the same heights as the children)
* we remove back colors (they were for testing), to add colors separate for each card we need an extra modifirer in a new class card__side--front-1 (with class nesting its not that bad). we set the colors add  some shadow to the card__side and fit rotateY(-180) in hover to make it rotate in correct side
* we start styling the front side of the card. we want 3 areas (div) for which we create 3 classes with element specialization (from BEM)
* we work on the 1st area *card__image* which we add a background image. we give a one spave text. and we set the height. to add 3 different images on each card we add a modifier. we set the backgorund image as linear gradient and url for the image. to add a cool effect on the common class we add anew feat `background-blend-mode: screen;`. also we set the background-size to cover so that the image streches in all area
* the card_side had border-radius. the image is squared and covers the rounded corner. to fix this we add to the parent element (card__side) overflow:hidden to cut the overflow.
* we add clip-path to add the polygon effect of the header. (we can make it a mixin)
* we style the second area *card__heading*. semanticaly it is a h4 so we change it from div to h4.
* we want it over the image so we give it postion absolute and give it a distance from the borders. we style the text. 
* as we want line breaks and gradient on each line we want to use the css property box-decoration-break. to use it we add a span *card__heading-span* and a modiffier per card *--1* for the different colors.
* we set the width in the heading and add padding to limit the size and enforce the line break. we add background-mage a linear gradient and use vox-decoration-brak in the spa to efore the rule to all boxes in teh the same selector (2 lines of text)
* in card details we make a ul list. we style it and positioon it with relative vaues. to center a box element in a box element we use `margin: 0 auto`
* we have to style the back of the card. it has only a white button which we have already as a component and some text. we create a div container under name *card__cta* and position it absolute and center it with the method we used in header
* button adapts to the width of the cta and has awkward small width because cta has no width , takes it from the element is contains (text). we give it a width

## Lecture 42 - Building the stories section. Pt.1

* Lecture objectives: how to make text flow around shapes with *shape-outside* and *float*, How to apply a *filter* to images,How to create a backround video covering an entire section, how to use the *<video>* HTML element, how and when to use the *object-fit* property
* we create anew section with a h2 heading and a story class div. the h2 we cp from another section. the section we add to our _home partial and do basic styling. for the *story* class we make a new component file named *_story.scss*
* we want to place a round image on teh left and an h3 and a paragraph on the right with text wrapping around the image. we start by adding a *figure* (semanticaly an image with caption) with class *story__shape*
* the figure is given fixed dimensions and positioned in a float . this enables us to use the *shape-outside* property to shape everything around it in a wrap by giving the vector (a circle). to use it we shape the figure by clipingit to a circle. again by a circle. the circle in css is defined by its radius and center. as we use absolute dimensions we can define them relative at 50% `shape-outside: circle(50% at 50% 50%);` to move the clipped figure to the left to create distance we dont use padding or margin. we never use these on modified elements . we use trsform: translatX or Y. the image is given a heiogth of 100% . if we used width it would not show correclty. 
* to skew the whole story we use skewX . but we cannot reverse skew the content by applying `& > * { transform: SkewX();}` as CSS dooes not inherit a second transformation in an already trasfomed element. we do this in each child adding the trasform.
* we will add blur effect and zoom out tot he image and fade in to the text on the image
* there is a special html element *figcaption* for image captions
* we givi it absolute positioning and we center it using the header technique. we add to the parent postion: relative to work. we style the text  and we traslate the text down on the Y axis giving an opacity of 0. 
* we add a hover rule to the parent element applying to children the *story_img* and *story_caption*. in caption hover we add opacity one and transform of tralslating the postion to the original (-50% -50%) to the center of the shape. to the img at normal state we scale it and move it left abit with translate tot center the woman. 
* in image hover we add two *filter* blur by 3px and brightness of 80%.
* we add transitions to the img and caption.
* to solve transition glitch we add backface-visibility hiden to image and caption and overflow: hidden to the parent element
* to add a video we add a container div abocve the h2 heading which we name bg-video and make it a component. we insert in it a hetml5 video element which wraps its source which are two format of the video .

```
<video class="bg-video__content" autoplay muted loop>
                        <source src="img/video.mp4" type="video/mp4">
                        <source src="img/video.webm" type="video/webm">
                        Your browser is not supported!
                    </video>
```
* the video attributes are for playback options
* we position the container with absolute position on top left corenrgiving a width and height of 100%. we put it behind with zindex and make it fade with low opacity.
* we give the parent class a position relative required to work with absolute positioning o the child
* the video per se bg-video__content we give it width and height of 100% and we ask it to cover the parent (like background-size: cover) with `object-fit:cover;`, this creates overflow which we tackle with overflow: hidden on the parent container.

## Lecture 45 - Building the Booking Section. Pt.1

* Lecture objectives: how to implement *solid-color-gradients*, how the general and adjacent sibling selectors work and why we need them, how to use the ::input-placeholder pseudo element, how and when to use the : focus, :invalid,  pseudoholder-shown and :checked pseudoclasses, techniques to build custom radio buttons
* we create a new section and a container for styling the background of our form. we consider it page specific so all of these go to _home partial
* the reusable part will be the form styling which will go to a separate partial.
* the pabground of the container *book* class is an image which we overlay with a linera gradient. we take advantage of two feats of the gradient. instead of tobottom and such we use *105deg* angle for finer control on direction. also we can add multiple stops on gradient by addint the percentage after the color. we use .9 opacity in rgba in 0% and 50% and we add one more stop of transparent at 50% to clear out. 
* background-size of 100% is the same as cover. 
* our book_form container class ofr the form takes 50% of the background image and has padding. in the container we add a form html tag of class form. in it we add two form_group classes for input label pairs and a reused div with h2 heading reused from assection
* we start styling the input we add the :focus pseudoclass to alter the apearance when clicked. we use the html input type to apply html5 validation using the :invalid pseudoclass to alter the borderbottom color when clicked and still invalid. to avoid move aup or down when notn click we add a transparent border line in normal state of input
* we style the label and we add an animation to make it disapear when placeholder is visible and make it appear when we have written something. we use the rule on input:placeholder-shown pseudoclass but we write it one level up to apply it to a different element. because label is a sibling (the next sibling) we use *+* and the element class. if it was just a sibling (not next in html) we would use *~*. this works because the label is after the input .if it was before in the html tree it would not work. to make it disapear we use visibility: hidden but to control the animation with transition we use opacity because this can be added to transition.
* some attributes like color are not inherited by default. to make them inheritable we use *inherit*
* we add anew form group for radio buttons. in it we add a container for each input + label pair. we give both radio inputs the same name to pair them (mutual exclusive)
* we want to style our own radio buttons. to do this we add a span in the label and we will hide the input
* we style form__radio-button span as a inline block element with specific height and width and border and border radius to look as a circle rim. we give it absolute position so parent element radio-label is relative.
* we create a pseudoelement::after to look as a circle and position it in the center of the main elelment circle rim. we default it to opacity 0. 
* we want to bind the transition of opacity to the actual radio-button. so we use selector `&__radio-input:checked ~ &__radio-label &__radio-button::after` using the checked pseudoclass of radioinput to get the state and apply it to the pseudoellemnt of span using the sibling selector and cascade.
* we hide the checkbox with display: none
* we add a button eleemnt and add the btn class to it. it is nt styled as in _button our selector was using pseudoclasses from the anchor tag not the button we add plain selector to the rule, we add focus to the active pseusodclass rule and we add a margin bottom utility to the form group above
* the rule is not applied as it is overwritten. to solve it we add !important to all utilities

## Lecture 48 - Building the Footer

* nothing new here
* to apply trasform the element must be block (inline-block or just block)
* inline-block takes the width of its content
* we use html semantic footer tag and a class which we style in layouts in a partial file

## Lecture 49 - Building the Navbigation Pt.1

* Lecture objectives: what the *checkbox hack* is and how it works, how to create custom aimation timing functions using cubic bezier curves, how to animate solid-color gradients, how and why to use *transform-origin*, in general create an amazing creative effect
* to do the button click reaveal navigation effect we will do a similar hack like in radio button but with checkbox. we will use the checkbox pseudoclass to capture the click but the checkbox will be invisible. what will be  visible and styled will be its label where the animations will be applied
* we will add a navigation div block over the header in html. in there we put a checkbox input a label adiv for background and a nav element with the list of links
* we style navigation in a layout partial of the same name
* we start from the background div. we give it a fix height and width, we make it round and we set position:fixed. this is like absolute but it doesnt change postiion when scaled or when page scrolls and alsothe iteme is taken out of the flow
* we make the same styling to the button but we give it a bigger size and higher z-index to cover the background.
* to make the background cover up we scale it by 80 times.  this with transform and binded to the hiodden checkbox will create the animation to present the nav
* the nav we make it fullscreen with vh without background and give it a high z-index.
* the links are given a background image of linear gradient with angle and stops. to crete the animation we change the background position
* to apply the animation when button is pressed we hide the background by removin gthe scale in default and hide navigation by setting nav to opacity: 0, as the cursor is still responding to nave even when hidden we add width: 0
* now we bind to checkbox checked pseudoclass applying it to a sibling. we use general sibling background and nav in separate rules to set the animation. 
* we see that navigation animation is wierd. we add width 100% to the list to fix that because when parend element loses its width the child (list sticks to right) we gan add background to nav to see it
* we will use custom timing function in our animation *cubic-bezier()*. there are online tools to work that easings.net. we see that playing with width in nav makes a nice transition
* the button icon effect will be fully custom. we hve three lines that are transformed into an X. the thre lines will be an element (middle) a pseudoelement :before (up) and :after (below)
* to make the icon we add a span in teh label (button class). we style the elemt and the 2 pseudoelements as small boxes . to make the pseudoelements appear we give them empty striung content. we make them inline-blocks to style them. location is wrong. we give them absolute positioninhg
* we bind to the checkbox checked pseudoclass. we dont change its width becaus ethis will affect the pseudoelements. we make it transparent
* transform-origin shows where the transformation happens. the point of reference. defualt is in the middle. right takes the right end.

## Lecture 52 - Building a Pure CSS Popup - Pt.1

* Lecture Objectives: how to build a nice popup with only CSS, how to use the *:target* pseudo-class, how to create boxes with equal height using *display: table-cell;* how to create CSS text columns, how to automatically hyphenate  words using *hyphens*

* we trigger the popup from reverse cards buttons
* we can put the popup anywhere in the markup
* when i say display:none to hide elements i cannot animate, i use opacity: 0 and visibility: hidden.
* anchor tags href can point to html ids using #idName
* when we want float right and left but the blocks have not the same diensions and we want alignement we prefer to display them as table-cells usw vertical-align and their parent to be set at display: table
* latest css allows columns to text with column-count (num of columns) column-gap and column-rule (border line vertical). also it allows `hyphens:auto;` but this requires our language to be set at html doc.
* a nice way to trigger animations with anchor tags is to ad an id to the element se this id to the href of the anchor. when clicked the tagret of the click event becomes the elemnt that has the id. we can use the &:target pseudoclass on the element (or its class) to style a transition when the anchor is clicked .e.g. change visivbility
* we cannot stack transforms. if we cannot put them all together because e.g of mixins we repeat the transforms of the e.g mixin in our secont transform

# Section 6 - Natours Project - Advanced Responsive Desing (Part 3)

## Lecture 54 -  Mobile-First vs Desktop First and Breakpoints

* Desktop First: Design for large screens -> then use media queries with max-width to adapt to smaller screens
* Mobile first: Design for mobile -> use media queries with min-width to adaptt to larger screens. enforces simplicity
* Media query : `@media(min-width: 500px) {}`
* typical breakpoints 0 - 600px - 900px -1200px - infinity
* media queries typically overlap  max-width: 900px overlaps 600px. CSS rules apply so typically we  write most specifuc rule last.
* MObile First: pros: 100% optimized for mobile, reduces website and app to the absolute essentials, result in smallerm faster more efficient products, content first. cons: desktop version empty and simplistic, difficult to develop,  less creative  frredom, clients want to see desktop version as prototype
* Think about if users use mobile, whats the purpose of the website
* Breakpoints: BAD APPROACH: using width of popular devices as breakpoints (usually Apple Products) GOOD APPROACH: find all popular devices of similar type and group them. place breakpoints among groups PERFECT APPROACH: ignore devices. put breakpoints where design breaks

## Lecture 56 - Use the Power of Sass Mixins to Write Media Queries

* Lecture Objectives: how to use a powerful sass mixing to write all our media queries, how to use the `@content` and `@if` sass directives, taking advantage of chrome devtools for responsive design.
* in the past the norm was to make a css file with media queries putin all rules per media query together.
* with sass we can put media queries in our selecor.
* it is still nonproductive to write the same media query in multiple rules. therefore we use mixins
* the approach is the following: in our _base partial we add a mixin 

```
@mixin respond-phone {
	@media (max-width: 600px) { @content };
}
```

* we use it in our rules like

```
@include respond-phone {
	font-size: 50%;
}
```

* @content is the css properties or code we wrap in include. we can use the ability of mixins to accept variables as parameters to parametrize the mixin calls
writing a media manager for all queries

```
@mixin respond($breakpoint) {
	@if $breakpoint == phone {
		@media (max-width: 600px) { @content };
	}
	@if $breakpoint == tab-port {
		@media (max-width: 900px) { @content };
	}
}
```

* and call it in our css with:

```
@include respond(phone) {
	font-size: 50%;
}
```

* we avoid using pizels in mdeia queries. em s and rem s in media queries are not affected by font-size we define but by the fontsize coming from the browser (16px)
we use ems as rems does not work in all browsers

* smaller query must go last. larger media queries first.
* we apply media queries in rem definition first. affecting all the design

## Lecture 57 - Writing Media Queries - Base, Typography and Layout

* we will get rid of white border as small screen
* we change typography sizes
* we follow with grid. the common change is to change col width to 100%
* we change margins
* we change bottom margin as stacked columns need space between
* also we have to decrease max width
* we go to header . we have to adapt clip path msking it smoother
* also in navigation the button size

* we see a white bar on the right when we decrease the width too much.
* we go to footer. we need to center everything when columns are stacked

## Lecture 58 - Writing Media Queries - Layout - About and Features Sections

* we see that we have too much padding in our layout. in home partial we reduce padding from sections
* we go now to components starting with composition
* we give images relative position floatrthem left and reduce their width. also we change positioning of indiuvidual pictures

## Lecture 59 - Writing Media Queries - Tours, Stories and Booking Sections

* we have to change the tour section. we have to hover over the card to flip and on mobile we have touch events. so we choose to skip the flip part and make all info apear on the front side. wthis is major refactoriung. actually whole component get rewriten. removing transitions , positioning shadows and sizes.
* in story component we make it square with width 100%. lower than 600 we have issue so we remove skew
* we go to booking section at home we increase form width , background-size (100% covers on x axis)

## Lecture 60 - An Overview of Responsive Images

* we have responsive images with vh sizes. but we are not there yet
* Responsive images mean: serve the right image to the right screen size and device , avoid downloading large images to small screens
* 3 use cases for responsive images: 
	* Resolution switcching. Large Screen -> Small screen (decrease image resolution on smaller screen)
	* Density Switching: @2x screen (high res) ->  @1x screen (low res) *H=aft the image resolution on @1x screen (pixel density)
	* Art direction: large screen -> small screen (different image on smaller screen)

## Lecture 61 - Responsive Images in HTML - Art Direction and Density Switching

* Lecture Objectives: How to use the *srcset* attribute on the *<img>* and *<source>* elements, together with density descriptions, how and why to use the *<picture>* element for art direction, how to write media queries in html
* in images in html we need the img tag of html (not background css image)
* we will do art direction and desity switching in footer logo
* we need 2 images for art direction

```
<img src="img/logo-green-2x.png" alt="Full logo" class="footer__logo">
```

* becomes the code below in density switching where we choose between 2 images on density 1x and 2x. using srcset instead of src

```
<img srcset="img/logo-green-1x.png 1x, img/logo-green-2x.png 2x" alt="Full logo" class="footer__logo">
```

* for art direction we use picture. it wraps source to apply a media query . when this is true we show the img in src. when it is false we show the follwoung img tag. we can combine it with desity switching like in the example

```
<picture class="footer__logo">
    <source srcset="img/logo-green-small-1x.png 1x, img/logo-green-small-2x.png 2x" media=(max-width: 37.5rem)">
    <img srcset="img/logo-green-1x.png 1x, img/logo-green-2x.png 2x" alt="Full logo">
</picture>
```

## Lecture 62 - Responsive Images in HTML - Density and Resolution Switching

* Lecture objectives: how to allow the browser to decide the best image to download, using the *srcset* attribute, width descriptors ante *sizes* attribute of the <img> element
* in chrome dev tools top right cornet we can adjust our pixel ration to test low res.
* we will apply the technique to the about section images
* we have two versions (1 with 1000px width and one with 300px width)

```
<img src="img/nat-1-large.jpg" alt="Photo 1" class="composition__photo composition__photo--p1">
```

* becomes

```
<img srcset="img/nat-1.jpg 300w, img/nat-1-large.jpg 1000w" 
     sizes="(max-widthL 900px) 20vw, (max-width: 600px) 30vw, 300px"
     alt="Photo 1"
     class="composition__photo composition__photo--p1"
     src="img/nat-1-large.jpg"
>
```

* there we apply res switching using the srcset instead of pixel density we give the actual width of the 2 images in pixels and in size we inform the browser of the breakpoints with max0width and the percentage of the image in vw for each breakpoint. we keep src for leagcy. browser will decide which to use to optimize performance. the browser will use the picture we specify in the breakpoint

## Lecture 63 - Responsive Images in CSS

* Lecture objectives: how to implement responsive images with CSS, how to use resolution media queries to target high-resolution screens with 2x, how to combine multiple conditions in media queries
* we will target header background image. we have one additional hero-small.jpg image with width 1000px. original is 2000px.
* we write a rule with media queries targeting resolution to use a better quality image for higher density screens `@media (min-resolution: 192dpi) {}`. we can combine media queries `@media (min-resolution: 192dpi) and (min-width: 600px)` or condition is applied with a comma and the second media query condition

## Lecture 64 - Testing for browser support with @supports

* Lecture objectives: how to use *@supports* feature queries, implement graceful degradation on selected properties, how to use the *backdrop-filter*
* backdrop-filter: blur(10px); (background blur) does not work in chrome only in safari
* the approach is to query and then apply

```
	@supports (-webkit-backdrop-filter: blur(10px)) or (backdrop-filter: blur(10px)) {
		backdrop-filter: blur(10px);
		-webkit-backdrop-filter: blur(10px);
		background-color: rgba($color-black, .3);
	}
```

* safari does not support media queries to resolution we add `(-webkit-min-device-pixel-ratio: 2)` which is supported
* cli-path does not work in safari

## Lecture 65 - Setting Up a simple build process using the NPM scripts

* main.sass -> [compilation] -> style.comp.css ->[concatenation]-> style.concat.css + icon-font.css->[prefixing]->style.prefix.css->[compressing]->style.css 
* production.code
* we will do all these in package.json.
	* first we change compile: sass name to watch:sass
	* we add "compile:sass": "node-sass sass/main.scss css/style.comp.css"
	* we install concat npm install concat --save-dev
	* we add "concat:css": "concat -o css/style.concat.css css/icon-font.css css/style.comp.css",
	* we install npm install autoprefixer --save-dev
	* we install  npm install postcss-cli --save-dev
	* we add "prefix:css": "postcss --use autoprefixer -b 'last 10 versions' css/style.concat.css -o css/style.prefix.css"
	* we install npm install npm-run-all --save-dev
	* we add a script "build:css": "npm-run-all compile:sass concat:css prefix:css compress:css"
	* we run npm run build:css
	* we add

```
    "devserver": "live-server",
    "watch:sass": "node-sass sass/main.scss css/style.css -w",
    "start": "npm-run-all --parallel devserver watch:sass",
```

## Lecture 66 - Wrapping Up. Final Touches

* highlight selected text. add this to base partial

```
::selection {
	background-color: rgba($color-primary, .5);
	color: $color-white;
}
```

* apply media queries only to screens (e.g. not in printouts) `@media only screen and (min-width: 112.5em) `
* we have to make sure our html has in its header the tag ` <meta name="viewport" content="width=device-width, initial-scale=1.0">` otherwise responsive design wont work
* our cards change style (no hover) in narrow screens. but in tabs in landscape we see the flip cards even we are on device. in css we can have media query to know if we can hover or not and style accordingly
* we cannot add to the media query in card parial becaus4 it is a mixin so we write it from start

```
@media only screen and (max-width: 56.25em),
		only screen and (hover: none) {}
```
* if we want to implement the navigation (close the navigation and point to the section) we need to write javascript. we cannot do this with css alone
* to close th popup when clicking outside the box we need to use javascript

# Section 7 - Master Flexbox

## Lecture 68 - Flexbox Overview

* What is: Flexbox is a new module in CSS3 that makes it easy to align elements to one another, in different directions and orders
	* the main idea behind flexbox is to give the container the ability to expand and to shrink elements to best use all the available space
	* flexbox replaces float layouts, using less and more readable logical code
	* it completeley changes the way we build one dimensional layouts
	* it is a true revolution in CS
* the element on which we use flex is called flex container. in this we add property `display: flex;` to behaves like an inline element (display: flex-inline) but rarely used as such
* all the children elements on which flex is applied are called flex items.
* the direction on xhich these elements are laid out is called main axis. the other perpenticular axis is called the cross axis
* we can select the direction of the main axis
* Main Flex Container Properties:
	* `flex-direction: row | row-reverse | column | column-reverse` selects the main axis direction
	* `flex-wrap: nowrap | wrap | wrap-reverse` determines if the items should wrap if there is not enough space in the main axis
	* `justify-content: flex-start | flex-end | center | space-between | space-around | space-evenly` specifies how items are aligned in the main axis
	* `align-items: stretch | flex-start | flex-end | center | baseline` specifies how items are aligned in the cross axis
	* `align-content: stretch | flex-start | flex-end | center | space-between | space-around` this prop applies when there are more than one rows of items and specifies how the rows of items will be aligned along the cross axis
* Main FLex Item Properties:
	* `align-self: auto | stretch | flex-start | flex-end | center | baseline` specifies the alignment of a specific item on the  cross axis. it overrides the flex container align for this item
	* `order: 0 | <integer>` manual set order of item
	* `flex-grow: 0 | <integer>` let flex decide on the width of the item (how mucxh it will grow)
	* `flex-shrink: 1 | <integer>` let flex decide on the width of the item (how mucxh it will shrink)
	* `flex-basis: auto |<length>`  let flex decide on the items base width
	* the last 3 properties are grouped together with flex: 0 1 auto | <int> <int> <length>

## Lecture 69 - Basic Intro to Flexbox - Flex Container

* Defaults: `flex-direction: row; justify-content: flex-start; align-items: stretch`
* justify content doesnt do anything for space between items. it is defined by the margin we define on the item and the container padding, only when we define space- we overwrite them. -betwwen distributes evenly space only between items -evenly around items (start end). and -around (gives 2x between and x in star and stop)
* align items aligne them in cross axis. strech stretches all to match the bigger height , center start and end are obvious. baseline aligns the text baseline in the items

## Lecture 70 - Basic Intro to Flexbox - Flex Items

* align self ovewrites aling-items for this item
* to put an item in the beginning i put order to -soemething. or lower than the others. flex orders by order number lower to higher. default is `order: 0;`
* by `flex-grow: 1;` items expand to occupy as much space as they can. the number is proportinal to the other items number. e.g if one has flex-grow: 1 and the other flex-grow: 2 the second is double the size in both dimensions than the other. flex-grow: 1 is the same as flex: 1 
* if we give flex:1 to one item and the other none then this one item stretches and the others no.
* flex-basis sets the width of the item. if we give e,g 20% it ocupies 20% of the available space. 100% is same as flex: 1 but in width axis . flex-basis wins over flex. 
* even if we fix the flex-basis to a set width in px when there is no available space it will shrink accordingly
* flex-shrink determines the items ability to shrink. default is flex-shrink: 1 meaning that the item can shrink. if we set it to 0 the item is not allowed to shrink
* flex: 0 means we dont want the item to grow. flex: 0 0 300px; means the item cannot grow or shrink and its width is 300px

## Lecture 71 - Basic Intro to Flexbox - Adding More Flex Items

* flex-wrap default value is no-wrap. wrap is adding a new line for the items that do not fit (without shrinking them?!?)
* the distance between rows is controled by aling-content: (defualt value of stretch which stretches the row height).

## Lecture 72 - Project Overview

* trillo. all in one booking app wireframe. flexbox + svg + animations
* we cp starter code from github
* we have a boilerplate project with sass and package.json ready with scripts
* we npm install dependencies
* modify our package.json
* run npm start
* we test that all dev flow works ok.

## Lecture 73 - Defining Project Settings and Custom Props

* lecture obj: how and why to use css custom props
* architecture: he wont follow 7 . 1 pattern. the project will be simple to focus on flexbox
* we add 3 scss files in sass. the partials _layout, _base and _component
* we start from base adding box-sizing to html rule and all elemets with * .
* we do initialization of styles in base and we want to set colors. we will not use sass variables like in last project. we will use css custom properties (css variables)
* with css we dont need preprosessor. we can manipulate them in javascript and we can edit them in dev tools
* css variables must be declared in a declaration box. like the global declaration block (*)
* css vars are available in the scope of the declaration they are defined and its children
* an easy place to gather them all is the root pseudoclass (:root)
* we define them with -- `--color-primary: #eb2f64;` we use them with var() `color: var(--color-primary);`
* we use linear-gradient as background image. we set background-size cover. it wraps the content (text) and repeats. we remove repetition with background-repeat: no-repeat.
* to stretch it in all screen we add height: 100vh; to accomodate larger screens . we add min-height: 100vh;

## Lecture 74 - Building the overall Layout

* Lecture obj: how to think about the overall layout in the app, use flexbox in a real-world project for the first time
* we have a huge container. on top it has a header with anavbar. under it on left a sidebar and on right the hotel view
* we add major layout eleemnts in our markup, give them classes and style them in the layout partial. (container, header,content, sidebar, hotel-view
* we style the container with max-width auto margins)
* we style the header with fix height 
* content class will be our flex container so we add property `display: flex;`
* we give the sidebar a fixed width 18% with no grow or shrink `flex: 0 0 18%;`
* we give the hotel-view the ability to shrink or grow and take as much space it can with `flex: 1;`
* we have to stretch in the cross axis

## Lecture 75 - Building the Header Pt.1

* Lecture objectives: why to use SVG icons vs font icons, how to find generate and use svg sprites in html, how to change the color of an SVG icon in CSS, how to use more advanced flexbox alignment techniques including justify-content, align-items, align-self and flex
* we add markup in header
* its a hack displaying icons that are images using fonts
* screen readers try to read icon fonts
* icomoon.io lets you upload an idon and make it svg or add an icon from a library
* he choses entypo+
* we generate a folder with 10 svg files for each icon and a general file symbol-defs.svg that contains all defs. we rename it as sprite.svg. we use it to have a single file to import in our html
* we import it using:

```
<svg class="search__icon">
    <use href="img/sprite.svg#icon-magnifying-glass"></use>
</svg>
```

* href works with a webserver
* we add a nav element with boxes to show icons on navbar
* to add notification like elements on icon we use span and a class (using the BEM naming convention)
* we style the header in components partial wher all BEM class hierarchies are styled
* svgs are styled like html elemetns when icon fonts are styled as text
* we use flexbox to put element side-by-side in the header so we use `display:flex;`
* we aligne item with justifycontent space-between
* we give a width to the search item using `flex: 0 0 40%;`
* we palce the search button on the input giving the input negative margin
* we center all items in search element using flex
* a flex item can become flex container
* we can change an svg color in css with *fill:*
* we use flexbox to align user-nav elements
* we use *&> ** selector to select all direct children
* we strtch all children using height:L 100% and the use flexbox to align the content of user-nav boxes
* we can use flex to align text as well

## Lecture 78 - Building the Navigation Pt.1

* Lercture Objectives: how to use scaleY and multiple transition properties with different settings, to create a creative hover effect, how and why to use the currentColor CSS variable, how to use some more advanced flexbox alignement techniques, including flex-direction, justify-content and align-items
* we add a ul with li items and a copyright text
* we give a large height to hotel-view to see the actual size of the navbar
* we change the direction of flex in sidebar and we apply flexbox on the container
* we use justify-content : space-between to push legal text to the bottom
* currentColor css variable is the color of the parent element or the current element
* we use flexbox to align list items
* in order to add the hover efect like a progress bar we add a before pseudoelement which will appear on hover
* transition can apply to more than 1 attributes
* to use z-index the element must have specified position
* using scaleY or X as transform attribute start the animation from center if we want an other point we can add trasform-origin

## Lecture 80 - Hotel Overview Pt.1

* how to create an infinite animation, how to use margin: auto with flexbox and why it is so powerful, continue to use flexbox properties for easy palcement and alignment
* we style image responsively giving them dimensions in % , also we display them as block to avoid white lines
* to create a big gap in the middle of the flex items we use flex: 1 to expand asingle one. but we want to create a signle gap without stretching. this is done with margin:auto. in our case margin-right
* svg items are inline elemtns and have a gap in height . either we use lineheight 0 and fontsize 0 or we style their parent element to flexbox
* in animation when wee declare infinate after the time it becomes an infinite animation

## Lecture 82 - Building the Description Section - Pt.1

* continue to use flexbox, including *flex-wrap* to build a multicolumn list, how and why to use CSS masks with *mask-image* and *mask-size*
* we use `flex-wrap: wrap;` to wrap flex item sin mulktiple lines and we use fixed width to each item
* we add svg in css as a background image
* the problem is that in that way we cannot change its color. to solve it we use masks
* masks create a shape through which we see the background color. currently it is supported in webkit browsers. -webkit-mask-image (like bagkground0-image) and -webkit-mask-size like background-size
* to add border without shrinking the image we use box-sizing: content-box and not border-box

## Lecture 84 - Building the Users Reviews Section Pt.1

* figure html elements are perfect for reviews
* text is a blockquote
* we add aglyph as pseydoelemt with ::before and style it

## Lecture 85 - Building the CTA Section

* we do acombination of transformY and top: -100% to hide and show alternatively 2 spans on a button

## Lecture 86 - Writing Media Queries Pt.1

* we will add breakpoints where design starts to break
* we remove the background color at 1200 with margin:0 to the container
* css varss do not work with media queries
* at 900 sidebar goes on top
* at 600 hotelview details go in column flex mode
* at 600 we need to fix the header, we will user flex order
* i give search order: 1 to move it last, we add flex-wrap to parent element and in search item we make flex: 0 0 100% to make it use whole row

# Section 8 - A QUick Introduction to CSS Grid Layouts

## Lecture 90 - Why CSS Grid: A whole new mindset

* CSS Grid Layout is a brand new module that brings a two dimensional grid system to CSS for the first time
* CSS Grid replaces float layouts , using less, and more readable and logical CSS and HTML
* CSS Grid works perfectly together with FLexbox, which is best for 1 dimension layouts and components
* CSS Grid completely changes the way that we envision and build two-dimensional layouts
* We apply it to a container (Grid COntainer by using `display: grid` or `display:grid-inline`)
* It uses a column axis and a row axis laying out the Grid Items (Container children)
* the horizontal and vertical lines that separate the container in rows and colymns are called grid lines and they are numbered automaticaly top to bottom and left to right the space between grid items is called gutter (alogn a line). the space between the lines is called grid track/row and grid track/column
* The area between 2 horizontal and 2 vertical grid lines is called grid area. the area between 2 adjacent grid vertical and horizontal lines is called grid cell
* firefox has the best devtools for css grid

## Lecture 92 - Create Our First Grid

* we can use chrome canary devtools as well/
* we create a container with 6 items. we make it a grid contianer with `display: grid;`
* we set the row and colum width with `grid-template-row: 150px 150px;` and `grid-template-column: 150px 150px 150px;`
* if the colmns and rows we define are not enough for the items we have they are left below.
* we define a gutter between rows with `grid-row-gap: 30px;` and between columns with `grid-column-gap: 30px;`. if we want the same gap everywhere we can use `grid-gap: `

## Lecture 93 - Getting Familiar with the *fr* unit

* instead of specifing width for each column/row we can use the repeat function  `grid-template-row: repeat(2, 150px);` we can mix  repeat with normal definition `grid-template-columns: repeat(2, 150px) 300px;`
* if we want to expand to fill the available space like `flex: 1` in flexbox we use the fractional unit in CSS grid. e,g, `grid-template-columns: repeat(2, 150px) 1fr;` we can distribute the space evenly with `grid-template-columns: repeat(3, 1fr);` of course we can set width with % to make it adaptive (% doesnt count the gap)

## Lecture 94 - Positioning Grid Items

* we can explicitly define the grid cell where an item will be place with row-start/end and column-start/end

```
    grid-row-start: 2;
    grid-row-end: 3;
    grid-column-start: 2;
    grid-column-end: 3;
```

* there is a shorthand version for the above syntax

```
    grid-row: 1/2;
    grid-column: 3/4;
```

* we can shorten it even further `grid-area: 1/3/2/4;`

## Lecture 95 - Spanning Grid Items

* to span my item in multiple cells i simply set the boundaries further e.g column-start: 2 and column-end: 4
* the items shift to an implicit grid. also items set a speciffic cell dont shift. this happens when the placement is not forced on a set cell. then it covers the cell 
* implicit grid has not set dimensions it is like inline.
* we can have multile grid items in a cell
* instead of setting end we can use span to set the number of cells span `grid-column: 1/ span 2;` is same as `grid-column: 1/ 3;`
* to span till the end (last line) we use -1 `grid-column: 2/ -1;`

## Lecture 98 - Naming Grid Lines

* we can name lines by putting their name in brackets before sizing and after sizing of cols/rows

```
grid-template-rows: [header-start] 100px [header-end box-start] 200px [box-end main-start] 400px [main-end footer-start] 100px [footer-end];
  grid-template-columns: repeat(3, [col-start] 1fr [col-end]) 200px [grid-end];
```

* in repeat before and after size naming is repeated lke col-start 1, col-start 2 etc
* we can use these names instead of numbers in our code

## Lecture 100  - Implicit Grids vs Explicit Grids

* the grid that we define with rows and columns is the explicit grid. the remaining grid items are positioned automatically by CSS grid in what we call implicit grid and is placed after the explicit grid. we can size the implicit grid with `grid-auto-rows: XX;` and `grid-auto-columns: XX;`
* by default implicit grid items are laid out in below the explicit grid. if we define `grid-auto-flow: column;` they are laid out in columns on teh right of the explicit grid
* implicit grid is perfect when we dont know how many items we will style 

## Lecture 101 - Aligning Grid Items

* like in flexbox we cal align the items with `align-items: `. this property aligns the grid item vertically in the grid area that is defined for it explicitly or implicitly. the default valu is stretch stretching item to cover all area.other vzalues are end,start,center
* we have `justify-items` that aligns items along the row axis horizontaly. the default value is stretch
* like flex we have `align-self:` property that align a specific item verticaly in its cell. in grid we hav elaso the `justify-self:`

## Lecture 102 - Align Grid Tracks

* to align the whole grid inside the grid container we use. for the horizontal axis `justify-content:` to the vertical axis `align-content:` 
* the allowed values like flexbox are: start / end / center / space-between / space-around / space-evenly
* if we want to avoid holes in our grid we use dense in our auto flow `grid-auto-flow: row dense;`

## Lecture - using the min-content, max-content and minmax() function

* max-content property is a sizing property in grid-template-column which sizes the cell according to the content tries to keep up with the content without causing any linebreak
* min-content sizes the column width to fit as much content as possible using linebreaks
* the two variables can be used for grid-templete-row as well with the same logic
* if cells have a fixed dimension and content doesnt fit it overflows
* minmax funtion gets 2 parameters min value and max value. css will adapt to the content size making sure that it stays within these two limits. if we use max or min-content as limit the size will adapt indefinetely from one side
* with relative container size frs adapt indefinetely. minmax() adpats within the set boundaries

## Lecture 104 - Responsive Layouts with auto-fit and auto-fill

* these are very powerfull tools for responsive design. we can use instead of a number in repeat() function the param auto-fill. this combined with a fixed size `grid-template-columns: repeat(auto-fill,100px);` will fit as many items as possible in the track given their size. this combined with a relative container size will make it responsive and fluid placing them according to the screen size. auto fill makes as many tracks as they fit in the container even if the items are not enough

* the difference with auto-fit is that auto-fit takes into account the available items and makes the grid large enough to fit them according to their size. this is done because emty cells collapse with a width of 0 `grid-template-columns: repeat(auto-fit, 100px);`
* realtive container size with a responsive item size (minmax(100px, 1fr)) creates responsive items and responsive layout to screen size
* this 2 combined with auto-row make a true adaptive design

```
width: 100vw;
display: grid;
grid-auto-rows:150px;
grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
```

# Section 9 - Nexter Project Master CSS Grid Layouts!

## Lecture 106 - Project Overview and Setup

* CSS Grid Layout responsive project
* one sass partial per component
*  in base.scss we add the initialization code

## Lecture 107 - Building the Overall Layout

* Lecture objectives: how to build a complex and modern layout using advanced CSS grid techniques, how to choose different row and column track sizes for different types of content
* we have a sidebar on left from top to bottom a wide header with two columns, below the header we have a 3 by 2 grid, below a 2 column section, below a 3 by 3 grid, below a complex css grid with photos and under a footer. 8 part layout
* we add the markup in html and give each element its own background color in its respective sass partial.
* we add display grin in the container ad add grid-template-row of 80vh. so we make an adaptive first row dependig on viewport. second row in min-content adaptive to content. 3rd row is adaptive to viewport width 40vw. 4row is adaptive to content (min-content). same holds for the last two (footer)
* we create 8 equaly sized columns ocuppying the viewport
* we want our 8 basic columns to be fixed sized so we divide typical 1200px to 8 and get 14rem. we want them adaptive so we give minmax(min-content, 140px) as we want a container of max width 1200px. the first colmn is fixed to represent the sidebar
* we add two flexible columns befor and after the 8 fixed to absorb the changes on viewport and keep the 8 fixed centered (full bleed sections)
* we name the lines
* we place the sidebar
* usually we name and size only the columns
* feats are occupying the 8 columns
* gallery and footer occupy full size
* homes only 8 columns
* header and story are split in aspecific column
* we see that frs go down to zero when shrinking the viewport. this pushes content to boundaries. we will use min max instead witha min of 6rem

## Lecture 109 - Building the Features Section Pt.1

* Lecture objectives: how and why to create grids inside grids, how to create responsive component without media queries, how to build a small component with CSS Grid
* we add 6 divs in features. we will make the feature grid item a grid container for the 6 feature classes.
* there is a technology for subgrids that snap their columns on the parent grid columns, this techology is not yet available.
* we add sizing and content in the inner grid
* we add css grid even to the feature itself to align icons (2*2 grid) even-though icon has a fixed width we use min-content to make it future proof (adaptive to possible new images)
* -1 means the end of the explicit grid. if we define no rows there is no explicit grid rows . only overflow. defining cell size with span solves it
* we aling feature text by adding align-items: start to features grid
* we will apply the grid fluid technique to make the features geid responsive without media queries `grid-template-columns: repeat(auto-fit, minmax(25rem, 1fr));`

## Lecture 111 - Building the story section - Pt.1

* Lecture Objectives: How to deal with overlapping grid items, why images are special and behave differently than other grid items, how to decide if flexbox is a better tool in certain situations
* we add markup and styling
* we dont hardcode margins in typography
* story_content is a one dimension layout so its better to use flexbox
* we do image position with grid. images are sized with 100% so they expand to the container size
* we make a 6* 6 grid to position our images
* we position photo on multiple rows and columns but it do not fill all area due to aspect-ratio

## Lecture 113 - Buildding the Homes Section - Pt.1

* Lecture Objectives: How to build a rather complex component using a mix of CSS Grid Properties, overlapping and Flexbox
* a grid of 6 (3 x 2) cards.
* we add markup and styling to each card, and we make it a grid with 2 columns
* we want button to span 2 columns but it as no BEM class so we add it
* we place the heart to the image using the grid overlapping feature. playing  with z-index
* placement algorithm does not automaticaly place items on top of each other. if we give no freedom to the algorithm specifying fully the area (row/column) the the algorithm will overlap elements `justify-self: end; margin: 1rem;` places the like heart in the corner

## Lecture 115 - Building the gallery - Pt.1

* Lecture objectives: how to create a complex grid looking gallery, using object-fit together with images for grid items
* when we have elements of various sizes to put in the grid the approach is to slect the row and column size to fit the smallest item. the number of lines is not fixed. it is try and error
* images maintain their aspect ratio when resizing. this is done by relating teh height to the vh while expandin the width
* we put pictures of various sizes in the grid. we add padding and line gap but still not perfect.
* if we use object-fit: cover on an object its like background-size: cover
* to make it work we need to add this: 

```
width: 100%;
height: 100%;
object-fit: cover;
display: block;
```

* we then set the grid cell size by column and row

## Lecture 119 - Building the Header

* Lecture Objetives: how to manage vertical spacing in a responsive layout using CSS Grid techniques, how to use ::before and ::after as grid items
* header has 80% of viewport height
* even text is a grid item .also pseudoelements ::before and ::after are grid items
* for image we use min-content and for text max-content to avoid line breaks
* for gaps we can use vh units to make them adaptive
* justify items to center title

## Lecture 122 - Writing Media Queries Pt.1

* we fix header first. the logos images will be made adaptive by making the height  max-height and setting a axi-width of 100%

```
	max-height: 2.5rem;
	max-width: 100%
```

* this doesnt work when we have set the column to max-content (tries to occupy max size). we change it to minmax(min-content, max-content)
* we apply minmax also to the text row to make it adaptive
* at 1200 we reduce rem def
* at 1000 we move the sidebar from column to row by rearanging master grid. we remove first column and add a new row
its good practice to name the columns and rows
* at 700 realtors and stories break. realtors go below header 
* at small screens we want min-content  size to adapt. if we remove size it is implicitly min-content (implicit grid)