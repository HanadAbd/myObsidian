2024-12-21 18:40

Status:

Tags: [[Web Development]]

---
Need to learn CSS because it's annoying me

Basics of Css, The CSS box model
--

Use the Box model. So for every element, it has **padding** that defines it's size, that has a **border** followed by **margin**, which is the negative space of the element, so moving the element across the document.
![[Pasted image 20250202152850.webp]]

So setting it to **border box** instead of content box, it will include padding and border


Flexbox:
--

Grid:
--

Good for multiple rows and columns 

```
display= grid;
gridTemplateColumns = "repeat(12, 1fr)"
gridAutoRows = "150px"
gap = "20px"
```

layout:
--

You can use flex box, so display flex soo all elements are flex children, and you can use **justfiy-content** for rows and **align items** for columns

we have a main axis that runs horizontally,  and cross that runs vertically. Any child elements will intially be added as rows but if you do flex-direction:column; it flips it to vertical


If you need more options, you can use grid, for more columns and rows. display: grid

use grid-template-columns: 1fr 1fr 1fr
so 3 evenly distributed columns

**Change width**:
--

Using Clamp to manage min,max,width

e.g. `width : clamp( 200px, 50%, 600px)`

min of 200px, max of 600px and preferred of 50%

display
--
most important, most default to:
- block- so starts a new line and goes as far left or right as it possibly can
- inline- section within the line (most common for like the a element since that's a link
- none- that's for things like scripts that shouldn't be rendered to the page

margin
--
margin: 0 auto : centres the div horizontally


Box Sizing:
--

In order to get around the issue of padding and borders increasing the size of elements and making harder to user, we tend to use:
Use this to not be as annoyed

* {
-webkit-box-sizing: border-box;
-moz-box-sizing: border-box;
box-sizing: border-box;
}

```
* {
    -webkit-box-sizing: border-box;
    -moz-box-sizing: border-box;
    box-sizing: border-box;
}
```

to specify that should always be that same size
![[Pasted image 20241023183046.png]]


Centring text and object in the middle or somewhere:
--

```
margin:auto
text-align:centre

margine-left: auto
text-align: left
```


##### References


----
