---
sidebar_position: 5
---
# Mixins

## Pass Mixins

Pass lets you create CSS code that is to be reused throughout the website.

## Defining a Mixin

Pass mixin Syntax:
```js
{  
  property:  value, 
  property:  value,
  ...  
}
```
> Note: `,` should be used instead of `;`

Or

```js
css`  
  property:  value;
  property:  value;
  ...
`
```
The following example creates a mixin named "important_text":

Pass Syntax:
```js
let important_text =  {  
  color:  'red',
  font_size:  '25px',
  font_weight:  'bold',
  border:  '1px solid blue'
}
```
> Note: use `_` instead of `-` in property names.
> Note: use double or single quotes around values to make them strings. Otherwise it's a syntax error.

 Or
```js
let important_text =  css`  
  color:  red;
  font-size:  25px;
  font-weight:  bold;
  border:  1px solid blue;
`
```

## Using a Mixin

The  `${mixin}`  syntax is used to include a mixin.

Pass include mixin Syntax:
```js
css`
selector {  
  ${mixin_name}
}
`
```
> Note: Don't add `;` after `${mixin_name}`.

So, to include the important_text mixin created above:

Pass Syntax:
```js
css`
.danger  {  
  ${important_text}  
  background-color:  green;  
}
`
```
  
Pass will convert the above to normal CSS:

CSS output:
```css
.danger  {  
  color:  red;  
  font-size:  25px;  
  font-weight:  bold;  
  border:  1px solid blue;  
  background-color:  green;  
}
```

A mixin can also include other mixins:

Pass Syntax:
```js
let special_text = {  
  ...important_text, 
  ...link, 
  ...special_border
}
```
Or
```js
let special_text = css` 
  ${important_text}
  ${link} 
  ${special_border}
`
```
  
## Passing Variables to a Mixin

With a simple change Mixins can accept arguments. This way you can pass variables to a mixin.

Here is how to define a mixin with arguments:

Pass Syntax:
```js
/* Define mixin with two arguments */  
let bordered = (color, width) => ({  
  border:  `${width} solid ${color}`
})  
// Or
/* Uncomment me
let bordered = (color, width) => css`  
  border:  ${width} solid ${color};
`
*/

.myArticle  {  
  ${bordered('blue', '1px') // Call mixin with two values
  }  
}  
  
.myNotes  {  
  ${bordered('red', '2px') // Call mixin with two values  
  }
}
```
  
Notice that the arguments are set as variables and then used as the values (color and width) of the border property.

After compilation, the CSS will look like this:

CSS Output:
```css
.myArticle  {  
  border:  1px solid blue;  
}  
  
.myNotes  {  
  border:  2px solid red;  
}
```

## Default Values for a Mixin

It is also possible to define default values for mixin variables:

Pass Syntax:
```js
let bordered = (color='blue', width='1px')  => ({  
  border:  `${width} solid ${color}`  
})
```
  
Then, you only need to specify the values that change when you include the mixin:

Pass Syntax:
```css
.myTips  {  
  ${bordered('orange')} 
}
```
  
## Using a Mixin For Vendor Prefixes

Another good use of a mixin is for vendor prefixes.

Here is an example for transform:

Pass Syntax:
```js
let transform = (property) => ({  
  _webkit_transform:  property, 
  _ms_transform:  property,
  transform:  property,
})
  
.myBox  {  
  ${transform(rotate('20deg'))}
}
```
  

After compilation, the CSS will look like this:

CSS Output:
```css
.myBox  {  
  -webkit-transform:  rotate(20deg);  
  -ms-transform:  rotate(20deg);  
  transform:  rotate(20deg);  
}
```