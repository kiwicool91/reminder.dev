# 👨🏻‍💻

> Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.

## Remove hsLang from url
```html
hs-skip-lang-url-rewrite
```

## Form Event
```js
window.addEventListener('message', event => {
	if (event.data.type === 'hsFormCallback' && event.data.eventName === 'onFormReady'){
		
	}
})
```
https://legacydocs.hubspot.com/global-form-events

## Custom Header
```jinja2
{% macro render_link_item(link,depth) %}
    {%- if link != [] && link.label -%}
    <li class="hs-menu-item hs-menu-depth-{{depth}} {{'hs-item-has-children' if link.children}}" aria-role="none" {{'aria-haspopup="true"' if link.children}}>
        <a href="{{link.url if link.url else '#'}}" aria-role="menuitem">{{link.label}}</a>
        {%- if link.children -%}
            <ul class="hs-menu-children-wrapper" aria-role="menu">
                {% set depth = depth + 1%}
                {% for sublink in link.children -%}
                    {{ render_link_item(sublink,depth) }}
                {%- endfor %}
            </ul>
        {% endif %}
        </li>
    {% endif %}
{% endmacro %}
<nav class="sc-site-header__menu sc-site-header__menu--{{ module.menu_field }} hs-menu-wrapper active-branch flyouts hs-menu-flow-horizontal" aria-label="{{menu_name}} menu">
    {% set menu = menu(module.menu_field , "site_root").children %}
    <ul aria-role="menubar">
    {% for link in menu %}
        {{ render_link_item(link,1) }}
    {% endfor %}
    </ul>
</nav>
```
## Appearance
```css
appearance: none;
-moz-appearance: none;
-webkit-appearance: none;
````

## Input Placeholder Color
```css
::-webkit-input-placeholder { /* Chrome/Opera/Safari */
  color: pink;
}
::-moz-placeholder { /* Firefox 19+ */
  color: pink;
}
:-ms-input-placeholder { /* IE 10+ */
  color: pink;
}
:-moz-placeholder { /* Firefox 18- */
  color: pink;
}
```

## Swipe detection
```js
document.addEventListener('touchstart', handleTouchStart, false);        
document.addEventListener('touchmove', handleTouchMove, false);

let xDown = null;                                                        
let yDown = null;

function getTouches(evt) {
  return evt.touches || // browser API
         evt.originalEvent.touches; // jQuery
}                                                     

function handleTouchStart(evt) {
    const firstTouch = getTouches(evt)[0];                                      
    xDown = firstTouch.clientX;                                      
    yDown = firstTouch.clientY;                                      
};                                                

function handleTouchMove(evt) {
    if ( ! xDown || ! yDown ) {
        return;
    }

    const xUp = evt.touches[0].clientX;                                    
    const yUp = evt.touches[0].clientY;

    const xDiff = xDown - xUp;
    const yDiff = yDown - yUp;

    if ( Math.abs( xDiff ) > Math.abs( yDiff ) ) {/*most significant*/
        if ( xDiff > 0 ) {
            /* right to left swipe ++ */ 
        } else {
            /* left to right swipe -- */
        }                       
    } else {
        if ( yDiff > 0 ) {
            /* up swipe */ 
        } else { 
            /* down swipe */
        }                                                                 
    }
    /* reset values */
    xDown = null;
    yDown = null;                                             
};
```

## Copy current URL to clipboard
```js
function insertSuccessPopup() {
	const successDiv = document.createElement('div');
	successDiv.textContent = "URL Copied";
	successDiv.setAttribute('class', 'success-div');
	document.body.append(successDiv);
	setTimeout(() => {
		successDiv.classList.add('fade-out');
		setTimeout(() => {
			successDiv.remove();
		}, 500)
	}, 2500)
}
	const shares = document.querySelectorAll(".blogpost__share-link");
	if (shares.length > 0) {
		shares.forEach(share => {
			share.addEventListener('click', () => {
				const tempInput = document.createElement('input');
				const url = location.href;
				tempInput.value = url;
				document.body.append(tempInput);
				tempInput.select();
				document.execCommand("copy");
				tempInput.remove();
				insertSuccessPopup();
			})
		})
	}
```

## Custom form module
```jinja2
{% form
	form_key="{{ name }}",
	form_to_use="{{ module.form.form_id }}",
	title="{{ module.form_title }}",
	no_title="{{ !module.add_title }}",
	response_response_type="{{ module.form.response_type }}",
	response_message="{{ module.form.message }}",
	response_redirect_id="{{ module.form.redirect_id }}",
	response_redirect_url="{{ module.form.redirect_url}}",
	gotowebinar_webinar_key="{{ module.form.gotowebinar_webinar_key }}",
	notifications_are_overridden="{{ module.notifications_are_overridden }}",
	notifications_override_email_addresses="{{ module.notifications_override_email_addresses }}",
	follow_up_type_simple="{{ module.follow_up_type_simple }}",
	simple_email_for_live_id="{{ module.simple_email_for_live_id }}",
	no_wrapper=true
%}
```

### Fields
* Form | form | form field
* Add title to the form? | add_title | boolean field
* Form Title | form_title | text field
* Send form notifications to specified email addresses instead of the form defaults | notifications_are_overridden | boolean field
* Email address | notifications_override_email_addresses | email address field 
* Send a follow-up email | follow_up_type_simple | boolean field
* Follow-up Email | simple_email_for_live_id | followup email field

## Custom counter for ordered list
```css
ol {
	padding-left: 2rem;
	counter-reset: counting-counter;
}
ol li {
	counter-increment: counting-counter;
}
ol li::before {
	content: counter(counting-counter) ". ";
	position: absolute;
	top: 0;
	left: -2rem;
	color: lightblack;
	font-weight: bold;
}
```
### With two digits before 🔟
```css
ol li:nth-child(-n+9)::before {
	content: "0"counter(offer-counter);
}
```

## Hover for desktop only
```css
@media (hover: none) and (pointer: coarse)
```

## Adaptive image with HubL resize function 
```jinja2
<img class="map-image" src="{{ module.hero_image.src }}" alt="{{ module.hero_image.alt }}" srcset="{{ resize_image_url(module.hero_image.src, 320)|replace(image_name, "") }} 320w, {{ resize_image_url(module.hero_image.src, 480)|replace(image_name, "") }} 480w, {{ resize_image_url(module.hero_image.src, 800)|replace(image_name, "") }} 800w" sizes="(max-width: 320px) 320px, (max-width: 480px) 480px, 800px" loading="lazy">
```

## Reset a cookie
```js
var rawCookie = document.cookie;
cookieArray = rawCookie.split(';');
cookieArray.shift();
function eraseCookie(name, domain) {   
    document.cookie = name+'=; expires=Thu, 01 Jan 1970 00:00:00 GMT; domain=' +domain+ '; path=/';  
}
for (var i = 0, len = cookieArray.length; i < len; i++) {
    var halfCookie = cookieArray[i].split('=');
    if (halfCookie[0] === ' hubspotutk') {
        eraseCookie('hubspotutk', '.markentive.com');
        eraseCookie('hubspotutk', '.hubspot.com');
        console.log(halfCookie);
    }
}
```

## Add Class pour CTA image
```js
let hsCtaCallbackInt = null;
function hsCtaCallback () {
    const tempCTAs = document.querySelectorAll('.hs-cta-wrapper a');
    if (tempCTAs.length > 0) {
        tempCTAs.forEach(tempCTA => {
            const CTAImage = tempCTA.querySelector('img');
            if (CTAImage) {
                tempCTA.classList.add('cta-has-image');
            }
        });
        clearInterval(hsCtaCallbackInt);
        console.log('CTA Loaded');
    }
}
hsCtaCallbackInt = setInterval(hsCtaCallback,1000); // A mettre dans un event DOMContentLoaded
setTimeout(() => {
    clearInterval(hsCtaCallbackInt);
}, 5000);
```

## Custom Language Switcher

https://community.hubspot.com/t5/CMS-Development/How-to-create-a-custom-language-switcher-in-HubL/td-p/199452
```jinja2
{% if content.translated_content and content.translated_content|length > 0 %}
<div class="header-lang">
    <nav class="language-switcher">
        <span class="language-switcher-current">{{ html_lang|upper }}</span>
        <div class="language-switcher-dropdown">
            {% for lang in content.translated_content %}
                {% if html_lang != lang.language %}
                <a href="/{{ lang.slug }}" class="language-switcher-link hs-skip-lang-url-rewrite" data-language="{{ lang.language }}" title="{{ lang.language|upper }}">{{ lang.language|upper }}</a>
                {% endif %}
            {% endfor %}
        </div>
    </nav>
</div>
{% endif %}
```

## Breadcrumb
https://community.hubspot.com/t5/CMS-Development/Customize-Breadcrumb-output/td-p/359570
```jinja2
{% set menu_id = module.renamed_from_id || module.menu %}
{% set node = menu(menu_id,"breadcrumb") %}

{# if node null means it's pretty much the home page, so don't display it #}
{% if node != null %}
<ul class="hs-breadcrumb-menu">

{# Add the home page in #}
{%  if node.level > '0' %}
    <li class="hs-breadcrumb-menu-item first-crumb">
        <a href="/" class="hs-breadcrumb-label">Home</a>
        <span class="hs-breadcrumb-menu-divider"></span>
    </li>
{% endif %}

{# Add the level in between if it's level 2 #}
{%  if node.level > '1' %}
    <li class="hs-breadcrumb-menu-item first-crumb">
        <a href="{{node.parentNode.url}}" class="hs-breadcrumb-label">{{node.parentNode.label}}</a>
        <span class="hs-breadcrumb-menu-divider"></span>
    </li>
{% endif %}

{# ADD the CURRENT PAGE #}
    <li class="hs-breadcrumb-menu-item last-crumb">
        <span class="hs-breadcrumb-label">{{node.label}}</span>
    </li>
</ul>
{% endif %}
```
* This includes HOME and will not display on the home page.
* To change the seperator, alls you need to do is:
```css
.hs-breadcrumb-menu-divider:before {
    content: '/'; //INSERT YOUR SEPARATOR HERE
    padding-left: 10px;
}
```
## Breadcrumb by mister T.
```jinja2
{% module "breadcrumbs" path="@hubspot/menu" root_type='breadcrumb' id="{{ menuId }}" label="Fil d'arianne" %}
```
> par contre il ne marche que dans le scope du header. l'id tu le prends dans l'url du menu dans les settings de hubspot

## Responsive Iframe (good old way)
```css
.resp-container {
    position: relative;
    overflow: hidden;
    padding-top: 56.25%;
}

.resp-iframe {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    border: 0;
}
```
## Layout CSS
```css
{% set gutter_width_percent = (16.6  * 100) / 1180 %}
{% set column_width_percent = (100 - (gutter_width_percent * 11)) / 12 %}

/* Responsive grid */
.row-fluid {display:flex;flex-wrap: wrap;}
.row-fluid [class*='span'] {margin-left: {{gutter_width_percent}}%;-webkit-box-sizing: border-box;-moz-box-sizing: border-box;-ms-box-sizing: border-box;box-sizing: border-box;}
.row-fluid [class*='span']:first-child {margin-left: 0;}
.row-fluid .span12 {flex: 0 0 auto;width: 100%}
.row-fluid .span11 {flex: 0 0 auto;width: calc( ({{column_width_percent}}% * 11) + ({{gutter_width_percent}}% * 10) );}
.row-fluid .span10 {flex: 0 0 auto;width: calc( ({{column_width_percent}}% * 10) + ({{gutter_width_percent}}% * 9) );}
.row-fluid .span9  {flex: 0 0 auto;width: calc( ({{column_width_percent}}% * 9) + ({{gutter_width_percent}}% * 8) );}
.row-fluid .span8  {flex: 0 0 auto;width: calc( ({{column_width_percent}}% * 8) + ({{gutter_width_percent}}% * 7) );}
.row-fluid .span7  {flex: 0 0 auto;width: calc( ({{column_width_percent}}% * 7) + ({{gutter_width_percent}}% * 6) );}
.row-fluid .span6  {flex: 0 0 auto;width: calc( ({{column_width_percent}}% * 6) + ({{gutter_width_percent}}% * 5) );}
.row-fluid .span5  {flex: 0 0 auto;width: calc( ({{column_width_percent}}% * 5) + ({{gutter_width_percent}}% * 4) );}
.row-fluid .span4  {flex: 0 0 auto;width: calc( ({{column_width_percent}}% * 4) + ({{gutter_width_percent}}% * 3) );}
.row-fluid .span3  {flex: 0 0 auto;width: calc( ({{column_width_percent}}% * 3) + ({{gutter_width_percent}}% * 2) );}
.row-fluid .span2  {flex: 0 0 auto;width: calc( ({{column_width_percent}}% * 2) + {{gutter_width_percent}}% );}
.row-fluid .span1  {flex: 0 0 auto;width: {{column_width_percent}}%;}

.container-fluid .row-fluid .wrapper,
.wrapper {
	margin: 0 auto;
	max-width: var(--wrapper-max-width);
	padding: var(--wrapper-padding)
}

@media (max-width: 768px) {
  .row-fluid [class*='span'] {
	  margin-left: 0;
		flex-shrink: 0;
		width: 100%;
		max-width: 100%}
}
```

## Returns the element height including margins
```js
function outerHeight(element) {
    const height = element.offsetHeight,
        style = window.getComputedStyle(element)

    return ['top', 'bottom']
        .map(side => parseInt(style[`margin-${side}`]))
        .reduce((total, side) => total + side, height)
}
```

## Edit property css in js
```js
let root = document.documentElement;

root.addEventListener("mousemove", e => {
  root.style.setProperty('--mouse-x', e.clientX + "px");
  root.style.setProperty('--mouse-y', e.clientY + "px");
});
```

## isMobile function with HubL
```jinja2
{% set agent = request.headers['user-agent']|lower|split(" ") %}
{% set isMobile = agent.index("mobile") > -1  ? true : false %}
```

## Hover Button
```css
button {
    0px 1px 1px 0px rgb(0 0 0 / 14%), 0px 2px 1px -1px rgb(0 0 0 / 12%), 0px 1px 3px 0px rgb(0 0 0 / 20%)
}
button:hover {
    0 2px 3px 0 rgb(60 64 67 / 30%), 0 6px 10px 4px rgb(60 64 67 / 15%)
}
```

## Scroll calcul
```js
const rect = ele.getBoundingClientRect();
const top = rect.top + document.body.scrollTop;

element.scrollTo({
  top: 100,
  left: 100,
  behavior: 'smooth'
});
```

## ScrollTo
```js
function getTopPosEl(elem) {
    const elemPos = elem.getBoundingClientRect()
    const top = (elemPos.top + window.scrollY) - headerEl.offsetHeight;
    return top;
}

function scrollToEl(elem) {
    window.scrollTo({
        top: getTopPosEl(elem),
        left: 0,
        behavior: "smooth"
    })
}
```

## Scroll to top

https://stackoverflow.com/questions/21474678/scrolltop-animation-without-jquery#answer-24559613

## Get the full height (include margin bottom)
https://stackoverflow.com/questions/10787782/full-height-of-a-html-element-div-including-border-padding-and-
```js
function getAbsoluteHeight(el) {
	el = (typeof el === 'string') ? document.querySelector(el) : el; 
	const styles = window.getComputedStyle(el),
	marginBottom = parseFloat(styles['marginBottom']);
	return Math.ceil(el.offsetHeight + marginBottom);
}
```

## Rebuilt URL with HubL Global Variables
```jinja2
<a href="{{ request.scheme}}://{{ request.domain }}/page">Link</a>
```

## One line and One column at same level
```css
.parent {
    display: grid;
    grid-template-columns: 1fr;
    align-items: start;
}
.child {
	grid-row-start: 1;
	grid-column-start: 1;
}
```

## Share article within a popup
```js
let WindowObjectReference = null;

if (popupButton) {

    function openRequestedPopup(strUrl, strWindowName) {
        const popupWidth = 700,
                    popupHeight = 700,
                    popupY = window.top.outerHeight / 2 + window.top.screenY - ( popupHeight / 2),
                    popupX = window.top.outerWidth / 2 + window.top.screenX - ( popupWidth / 2);
        if (WindowObjectReference == null || WindowObjectReference.closed) {
            WindowObjectReference = window.open(strUrl, strWindowName, `toolbar=no, location=no, directories=no, status=no, menubar=no, scrollbars=no, resizable=no, copyhistory=no, width=${popupWidth}, height=${popupHeight}, top=${popupY}, left=${popupX}`);

        }
        else {
            WindowObjectReference.focus();
        };
    }

    popupButton.addEventListener('click', (e) => {
        e.preventDefault();
        openRequestedPopup(popupButton.getAttribute('href'), 'popup-name');
        popupButton.classList.add('popup--hidden');
    })
}
```
* Facebook URL : `https://www.facebook.com/sharer/sharer.php?u={{ content.absolute_url }}`
* Twitter URL : `https://twitter.com/intent/tweet?original_referer={{ content.absolute_url }}%3Futm_medium%3Dsocial%26utm_source%3Dtwitter&url={{ content.absolute_url }}%3Futm_medium%3Dsocial%26utm_source%3Dtwitter&source=tweetbutton&text={{ content.name|striptags|urlencode }}`
* LinkedIn URL : `https://www.linkedin.com/shareArticle?mini=true&url={{ content.asbolute_url }}%3Futm_medium%3Dsocial%26utm_source%3Dlinkedin`

## Image with srcset and resize_image_url
```jinja2
{%- if module.image_field.src -%}
<img srcset="{{ resize_image_url(module.image_field.src, 288) }} 288vw,
    {{ resize_image_url(module.image_field.src, 468) }} 468vw,
    {{ resize_image_url(module.image_field.src, 736) }} 736vw,
    {{ resize_image_url(module.image_field.src, 928) }} 928w"
    sizes="(max-width: 320px) 288px,
            (max-width: 500px) 468px
            (max-width: 768px) 736px,
            928px"
    src="{{ modue.image_field.src }}"
    alt="{{ modue.image_field.alt }}"
    width="{{ modue.image_field.width }}"
    height="{{ modue.image_field.height }}"
    loading="lazy">
{% endif %}
```

## Does Parent has overflow hidden
```js
let parent = document.querySelector('.sticky').parentElement;

while (parent) {
    const hasOverflow = getComputedStyle(parent).overflow;
    if (hasOverflow !== 'visible') {
        console.log(hasOverflow, parent);
    }
    parent = parent.parentElement;
}
```

## Responsive resolutions

* Extra-extra-large
    * 5120x2880
    * 2560x1440
    * 1920x1200
    * 1920x1080
    * 1680x1080
    * 1600x900
    * 1536x864
* Extra-large
    * 1440x900
    * 1440x700
    * 1366x768
    * 1280x800
* Large
    * 1024x768
    * 1024x600
    * 960x540
* Medium
    * 992x1024
    * 800x1280
    * 800x480
    * 768x1366
    * 768x1024
    * 720x1280
* Small
    * 600x1024
    * 600x960
    * 540x960
    * 480x800
* Extra-small
    * 414x736
    * 400x640
    * 384x640
    * 375x667
    * 360x640
    * 360x720
    * 320x568
    * 320x533
    * 320x480

## Pulse Effect
```css
::before {
    content: "";
    position: absolute;
    z-index: 0;
    top: 50%;
    left: 50%;
    display: block;
    width: 4.75rem;
    height: 4.75rem;
    border-radius: 50%;
    background: #5f4dee;
    animation: pulse-border 1500ms ease-out infinite;
    transform: translate(-50%,-50%);
}
  
@keyframes pulse-border {
	0% {
		transform: translateX(-50%) translateY(-50%) translateZ(0) scale(1);
		opacity: 1;
	}
	100% {
		transform: translateX(-50%) translateY(-50%) translateZ(0) scale(1.5);
		opacity: 0;
	}
}
```
## Customiser Resubmit du formulaire
```html
<style>
  form.hs-form.has-resub {
    position: relative;
  }
  form.hs-form.has-resub ul.no-list.hs-error-msgs.inputs-list[role="alert"] {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    display: flex !important; /* because hubspot inline style ... */
    justify-content: center;
    align-items: center;
    z-index: 20;
    background-color: rgba(255,255,255, 0.75);
  }
  form.hs-form.has-resub ul.no-list.hs-error-msgs.inputs-list[role="alert"] a,
  form.hs-form.has-resub ul.no-list.hs-error-msgs.inputs-list[role="alert"] label {
    display: block;
    font-size: 2rem;
    line-height: 1.75;
    padding: 1rem;
    text-align: center;
    color: #635a79;
  }
  .blog-logo-menu-module .newsletter-container {
    position: relative;
  }
  .blog-logo-menu-module form.hs-form.has-resub {
    position: unset;
  }
  .blog-logo-menu-module form.hs-form.has-resub .field,
  .footer-module form.hs-form.has-resub .field {
    position: unset;
  }
  .blog-logo-menu-module form.hs-form.has-resub ul.no-list.hs-error-msgs.inputs-list[role="alert"] {
    top: 50%;
    height: 110px;
    background-color: rgba(99, 90, 121, 0.85);
    box-shadow: unset;
    padding-left: 1rem;
    transform: translate(0,-50%);
  }
  .blog-logo-menu-module form.hs-form.has-resub ul.no-list.hs-error-msgs.inputs-list[role="alert"] a,
  .blog-logo-menu-module form.hs-form.has-resub ul.no-list.hs-error-msgs.inputs-list[role="alert"] label {
    color: #FFF;
  }
  .footer-module form.hs-form.has-resub ul.no-list.hs-error-msgs.inputs-list[role="alert"] {
    background-color: rgba(234, 234, 234, 0.85);
    padding-left: 0rem;
  }
  .blog-logo-menu-module form.hs-form.has-resub ul.no-list.hs-error-msgs.inputs-list[role="alert"] a, 
  .footer-module form.hs-form.has-resub ul.no-list.hs-error-msgs.inputs-list[role="alert"] a,
  .blog-logo-menu-module form.hs-form.has-resub ul.no-list.hs-error-msgs.inputs-list[role="alert"] label, 
  .footer-module form.hs-form.has-resub ul.no-list.hs-error-msgs.inputs-list[role="alert"] label {
    font-size: 1.2rem;
    line-height: 1.5;
  }
</style>

<script>
  document.addEventListener('DOMContentLoaded', () => {
    const currentForms = document.querySelectorAll('.hs_cos_wrapper_type_form')
    let formCount = currentForms.length;

    window.addEventListener('message', event => {
      if(event.data.type === 'hsFormCallback' && event.data.eventName === 'onFormReady') {
        formCount--;
        if (formCount === 0) {
          const forms = document.querySelectorAll('form.hs-form');
          forms.forEach(form => {
            const ulError = form.querySelector('ul.no-list.hs-error-msgs.inputs-list[role="alert"]');
            if (ulError) {
              const tempErrorLink = (ulError.querySelector('a') || ulError.querySelector('label'));
              if (tempErrorLink && (tempErrorLink.textContent === "Vous avez demandé à ce que des notifications ne vous soient plus envoyées par e-mail. Cliquez ici pour recevoir un e-mail vous permettant d'en bénéficier à nouveau." || tempErrorLink.textContent === "Consultez votre boîte de réception pour recevoir à nouveau des notifications.")) {
                form.classList.add('has-resub');
              }
            }
            

            // Selectionne le noeud dont les mutations seront observées
            const targetNode = form;
            // Options de l'observateur (quelles sont les mutations à observer)
            const config = { attributes: true, childList: true };
            // Fonction callback à éxécuter quand une mutation est observée
            const callback = function(mutationsList) {
              for(var mutation of mutationsList) {
                if (mutation.type == 'childList') {
                  // console.log('Un noeud enfant a été ajouté ou supprimé.');
                  const currentError = document.querySelector('form.hs-form ul.no-list.hs-error-msgs.inputs-list[role="alert"]');
                  if (currentError) {
                    const currentErrorLink = (currentError.querySelector('a') || currentError.querySelector('label'));
                    if (currentErrorLink && (currentErrorLink.textContent === "Vous avez demandé à ce que des notifications ne vous soient plus envoyées par e-mail. Cliquez ici pour recevoir un e-mail vous permettant d'en bénéficier à nouveau." || currentErrorLink.textContent === "Consultez votre boîte de réception pour recevoir à nouveau des notifications.")) {
                      form.classList.add('has-resub');
                    } else {
                      form.classList.remove('has-resub');
                    }
                  }
                }
                {#
                else if (mutation.type == 'attributes') {
                  console.log("L'attribut '" + mutation.attributeName + "' a été modifié.");
                }
                #}
              }
            };
            // Créé une instance de l'observateur lié à la fonction de callback
            const observer = new MutationObserver(callback);
            // Commence à observer le noeud cible pour les mutations précédemment configurées
            observer.observe(targetNode, config);
          })
        }
      }
    })
  })
</script>
```

## Hover Effect
```css
button {
    box-shadow: 0 3px 5px 0 rgba(36, 50, 66, 0.2);
}
button:hover { 
    box-shadow: 0 11px 12px 0 rgba(36, 50, 66, 0.12);
} 

button {
    box-shadow: 0 10px 50px 0 rgba(84, 110, 122, 0.15);
}
button:hover {
    box-shadow: 0 10px 50px 0 rgba(84, 110, 122, 0.35);
}
```

## Smooth box-shadow
```css
popup {
    box-shadow:
    0 2.8px 2.2px rgba(0, 0, 0, 0.034),
    0 6.7px 5.3px rgba(0, 0, 0, 0.048),
    0 12.5px 10px rgba(0, 0, 0, 0.06),
    0 22.3px 17.9px rgba(0, 0, 0, 0.072),
    0 41.8px 33.4px rgba(0, 0, 0, 0.086),
    0 100px 80px rgba(0, 0, 0, 0.12)
    ;
}
```

## Column layout without pushing child when child expand
```css
.parent {
	columns: 2;
}
.child {
	-webkit-column-break-inside: avoid;
 	page-break-inside: avoid;
	break-inside: avoid-column;
}
```

## Generate Array with content of the H2 inside a blog post
```jinja2
{# replace h2 tags by easy readable markup #}
{%- set update_post_body = (content.post_body|regex_replace("<h2(.*?)>", "$$open$$"))|regex_replace("</h2>", "$$close$$") -%}
{# split the string previously created with the custom opening tag #}
{%- set split_post_body = update_post_body|split('$$open$$') -%}
{%- set heading_array = [] -%}
{% for item in split_post_body -%}
    {% if not loop.first %}
        {% if item is string_containing "$$close$$" %}
            {% do heading_array.append(item|split('$$close$$')|first|regex_replace("<!--(.*?)-->", "")) %}{# remove HTML comments as well #}
        {% endif %}
    {% endif %}
{%- endfor %}
```

## Form to know the reason of unsubscribe
```jinja2
<div class="form-unsub-container">
{% form
    	form_key="{{ name }}",
    	form_to_use="{{ module.form.form_id }}",
    	title="{{ module.form_title }}",
    	no_title="{{ !module.add_title }}",
			response_response_type="{{ module.form.response_type }}",
			response_message="{{ module.form.message }}",
			response_redirect_id="{{ module.form.redirect_id }}",
			response_redirect_url="{{module.form.redirect_url}}",
			gotowebinar_webinar_key="{{ module.form.gotowebinar_webinar_key }}",
			notifications_are_overridden="{{ module.notifications_are_overridden }}",
			notifications_override_email_addresses="{{ module.notifications_override_email_addresses }}",
			follow_up_type_simple="{{ module.follow_up_type_simple }}",
			simple_email_for_live_id="{{ module.simple_email_for_live_id }}",
			no_wrapper=True
%}
	
</div>
{% require_js, position="head" %}
<script>
	document.addEventListener('DOMContentLoaded', () => {
		window.addEventListener('message', () => {
			if(event.data.type === 'hsFormCallback' && event.data.eventName === 'onFormReady'){
				console.log('hey')
				const currentEmail = "{{ personalization_token('contact.email', 'default value')|render }}";
				const emailUnsubReasonForm = document.querySelector('.form-unsub-container form');
				
				if (emailUnsubReasonForm !== "" && emailUnsubReasonForm) {
					const unsubFormEmail = emailUnsubReasonForm.querySelector('input[name="email"]');
					unsubFormEmail.value = currentEmail;
					
				}
			}
		})
	})
</script>
{% end_require_js %}
```

## Intersection observer - Reveal on scroll
```js
const sections = document.querySelectorAll('.solutions.shazam .dnd-section');
if (sections.length > 0) {
    const sectionsObserver = new IntersectionObserver((entries, sectionObserver) => {
        entries.forEach((entry) => {
            if (entry.isIntersecting) {
                console.log(entry.target)
                // entry.target.classList.add(‘show');
                sectionsObserver.unobserve(entry.target);
            }
        })
    }, {
        threshold: 0.5
    });
    sections.forEach(section => {
        sectionsObserver.observe(section)
    })
}
```

## Styling the IDE HS
```css
@import url('https://cdn.jsdelivr.net/npm/victormono@latest/dist/index.css');
  
.CodeMirror pre {
  font-family: 'Victor Mono', monospace;
}

.CodeMirror-line .cm-tab {
  border-left: 1px solid rgba(203,214,226,.15);
}
```

## Read Time of a Blog Post
```jinja2
{%- set initialPostWords = content.post_body|striptags|wordcount -%}
{%- set calculatedPostWords = (initialPostWords/100) * 100 -%}
{%- set finishedPostWords = calculatedPostWords|divide(300)|round(2) -%}
{%- set number = finishedPostWords|round -%}
<time class="post__read-time d-flex align-items-center" datetime="PT{{ number }}M"><svg class="icon icon--clock"><use href="#clock"></use></svg><span>{{ number < 1 ? "1" : number }} min</span></time>
```

## Hash dans l’URL
```js
function offsetTop(el) {
    if (!el)
        return 0
    const rect = el.getBoundingClientRect(),
                scrollTop = window.pageYOffset || document.documentElement.scrollTop;
    return (rect.top + scrollTop)
}

if (location.hash) {
    setTimeout(function() {
        window.scrollTo(0, 0);
        const currentTitle = document.getElementById(location.hash.replace('#', ''));
        const currentPosTop = (offsetTop(currentTitle)) - (header.offsetHeight);
        // const currentPosTop = offsetTop(currentTitle);
        window.scrollTo({
            top: currentPosTop,
            left: 0,
            behavior: 'smooth'
        });
    }, 1);
}

window.addEventListener('hashchange', (e) => {
    console.log('hash change');
    e.preventDefault();
    const currentTitle = document.getElementById(location.hash.replace('#', ''));
    const currentPosTop = (offsetTop(currentTitle)) - (header.offsetHeight);
    // const currentPosTop = offsetTop(currentTitle);
    window.scrollTo({
        top: currentPosTop,
        left: 0,
        behavior: 'smooth'
    });
})
```

## Zoom in on Hover
```html
<style media="screen">
    figure.zoom {
        background-position: 50% 50%;
        position: relative;
        margin: 150px auto;
        border: 5px solid white;
        box-shadow: -1px 5px 15px black;
        height: 300px;
        width: 500px;
        overflow: hidden;
        cursor: zoom-in;
    }
    figure.zoom img:hover {
        opacity: 0;
    }
    figure.zoom img {
        transition: opacity 0.5s;
        display: block;
        width: 100%;
    }
</style>

<figure class="zoom" onmousemove="zoom(event)" style="background-image: url(https://i.pinimg.com/originals/2b/de/de/2bdede0647e3cdf75b44ea33723201d9.jpg)">
    <img src="https://i.pinimg.com/originals/2b/de/de/2bdede0647e3cdf75b44ea33723201d9.jpg" />
</figure>

<script type="text/javascript">
    function zoom(e){
        const zoomer = e.currentTarget;
        e.offsetX ? offsetX = e.offsetX : offsetX = e.touches[0].pageX
        e.offsetY ? offsetY = e.offsetY : offsetX = e.touches[0].pageX
        x = offsetX/zoomer.offsetWidth * 100
        y = offsetY/zoomer.offsetHeight * 100
        zoomer.style.backgroundPosition = x + '% ' + y + '%';
    }
</script>
```

## URL API
```js
const url = new URL(window.location);
url.searchParams.set(key, value);
url.searchParams.delete(key);
window.history.pushState(null, '', decodeURIComponent(url.toString()));
```

## Circle with css
```css
div {
    background-image: radial-gradient(width circle at xpos ypos, #FFF 50%, transparent 51%);
}
```

## Custom Form Redirection
```jinja2
<div class="form-redirection{{ " form-redirection--has-image" if module.add_side_image and module.side_image.src }}">
	<div class="container">
		{% if module.add_side_image and module.side_image.src %}
		<div class="form-redirection__col form-redirection__col--image">
			{% if module.side_image.src %}
			{% set sizeAttrs = 'width="{{ module.side_image.width }}" height="{{ module.side_image.height }}"' %}
			{% if module.side_image.size_type == 'auto' %}
			{% set sizeAttrs = 'style="max-width: 100%; height: auto;"' %}
			{% elif module.side_image.size_type == 'auto_custom_max' %}
			{% set sizeAttrs = 'width="{{ module.side_image.max_width }}" height="{{ module.side_image.max_height }}" style="max-width: 100%; height: auto;"' %}
			{% endif %}
			<img class="form-redirection__side-image" src="{{ module.side_image.src }}" alt="{{ module.side_image.alt }}" loading="lazy" {{ sizeAttrs }}>
			{% endif %}
		</div>
		{% endif %}
		<div class="form-redirection__col form-redirection__col--form">
			{%- if module.title != "" -%}
			<h2 class="form-redirection__title">{{ module.title }}</h2>
			{% endif %}
			{%- if module.text != "" -%}
			<div class="form-redirection__text">
				{{ module.text }}
			</div>
			{% endif %}
			<div class="custom-form" data-form-key="form-redirection-{{ name }}">
				{% form
				form_key="form-redirection-{{ name }}",
				form_to_use="{{ module.form.form_id }}",
				response_response_type="{{ module.form.response_type }}",
				response_message="{{ module.form.message }}",
				response_redirect_id="{{ module.form.redirect_id }}",
				response_redirect_url="{{module.form.redirect_url}}",
				gotowebinar_webinar_key="{{ module.form.gotowebinar_webinar_key }}",
				no_wrapper=true
			%}
			</div>
		</div>
	</div>
</div>
{%- set content_page = content_by_id(module.page) -%}
{% require_js -%}
<script>
	const formId = "{{ module.form.form_id }}",
	pageUrl = "{{ content_page.absolute_url }}";
	
	let query = "",
			currentFormId = "",
			currentFormContainer = null;
	// get the current form submited and his container
	window.addEventListener('submit', (e) => {
		currentFormId = e.target.dataset.formId;
		currentFormContainer = e.target.closest('.custom-form[data-form-key="form-redirection-{{ name }}"]');
	})
	
	window.addEventListener('message', event => {
		if (event.data.type === 'hsFormCallback' && event.data.eventName === 'onFormSubmitted'){
			// check if the current form submited is the form of our custom module 
			if (event.data.id === currentFormId && currentFormContainer) {
				event.data.data.forEach((data, index, array) => {
					{% for param in module.params -%}
					if (data.name === "{{ param.param }}") {
					  {% for value in param.value_query -%}
						if (data.value === "{{ value.value }}") {
							query = query === "" ? `?{{ param.param }}=${ "{{ value.query }}" }` : `${query}&{{ param.param }}=${ "{{ value.query }}" }`;
						}
						{%- endfor %}
					}
					{%- endfor %}
					if (index === (array.length - 1)) {
						window.location = `${ pageUrl }${ query }`;
					}
				})
			}
		}
	})
</script>
{%- end_require_js %}
```

## Animate Number
> https://animejs.com/
```js
if (typeof anime === "function"){
    el.textContent = formatValue(endValue)
    anime({
        targets: el,
        textContent: [previousValue, endValue],
        round: incrementor ? 1/incrementor : 1/100,
        easing: 'easeInOutQuad',
        duration: duration ? duration : 1000,
        update: function(a) {
            const value = a.animations[0].currentValue;
            const formattedNumber = formatValue(value);
            el.innerHTML = formattedNumber;
        },
        begin: function(a) {
            const value = a.animations[0].currentValue;
            const formattedNumber = formatValue(value);
            el.innerHTML = formattedNumber;
        }
    });
}
```

## Keep order in content_by_ids
```jinja2
{% set posts = [39695648330, 39696525604, 39985330401, 39696525816] %}
{% set objects = content_by_ids(posts) %}
{% for post in posts %}
    {% for key, object in objects.items() %}
        {% if key == post %}
            {{ object }}
        {% endif %}
    {% endfor %}
{% endfor %}
```

## Custom carousel

TODO

## Load a script
```js
const loadScript = (src, async = true, type = 'text/javascript') => {
  return new Promise((resolve, reject) => {
    try {
      const el = document.createElement('script')
      const container = document.head || document.body

      el.type = type
      el.async = async
      el.src = src

      el.addEventListener('load', () => {
        resolve({ status: true })
      })

      el.addEventListener('error', () => {
        reject({
          status: false,
          message: `Failed to load the script ${src}`
        })
      })

      container.appendChild(el)
    } catch (err) {
      reject(err)
    }
  })
}

loadScript(‘main.js')
  .then(data => {
    console.log(‘Script loaded successfully', data)
  })
  .catch(err => {
    console.error(err)
  })
```

## Show for Screen Reader
```css
.show-for-sr {
  border: 0 !important;
  clip: rect(0, 0, 0, 0) !important;
  height: 1px !important;
  overflow: hidden !important;
  padding: 0 !important;
  position: absolute !important;
  white-space: nowrap !important;
  width: 1px !important;
}

@media (max-width: 767px) {
  .show-for-sr--mobile {
    border: 0 !important;
    clip: rect(0, 0, 0, 0) !important;
    height: 1px !important;
    overflow: hidden !important;
    padding: 0 !important;
    position: absolute !important;
    white-space: nowrap !important;
    width: 1px !important;
  }
}
```