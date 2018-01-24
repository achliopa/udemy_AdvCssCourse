
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
