
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