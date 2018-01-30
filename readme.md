
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