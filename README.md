# vml-and-accessibility
Some accessibility tests on VML components


## VML component :  v:oval
### VML component :  v:oval without Alt

```
<!--[if mso]>
  <v:group>
    <v:arc/>
    <v:arc/>
    <v:oval>
      <center>
        <h1></h1>
       </center>
  </v:group>
<![endif]-->
```
Outlook keeps all the vml code by adding a whole bunch of attributes in the process. It adds an ID to the component, like so:

```
 <!--[if gte vml 1]><v:group  id="_x0000_s1040"></v:group><![endif]-->
```

As a result, it produces an image, like this :

```
<!--[if !vml]--><img width="200" height="200" src="file:////msohtmlclip1/01/clip_image001.png" v:shapes="_x0000_s1040 _x0000_s1041 _x0000_s1042 _x0000_s1043"><!--[endif]-->
```

Without an Alt attribute on the VML component, the image displayed in the Inbox contains no information. If there is text inside the component, it is not read by screen readers

### VML component :  v:oval with Alt

```
<!--[if mso]>
<v:group alt="1-Our work">
  <v:arc/>
  <v:arc/>
    <v:oval>
      <center>
        <h1>1-Our work</h1>
      </center>
    </v:oval>
  </v:group>
<![endif]-->
```


By adding an Alt attribute on the VML component, Outlook keeps that Alt in code, and it also carries it over to the image it creates for display. The screen reader reads the information.

## VML component :  v:roundrect
### VML component :  v:roundrect without Alt

Here we reproduce a rounded HTML image, in its VML version. So there are two versions of the same image, one for Outlook, and one for the rest

```
<!--[if mso]>
<v:roundrect>
  <v:fill src="https://picsum.photos/670/400" type="frame"/>
</v:roundrect>
<![endif]-->
```

Without Alt attribute added to the v:fill element, the screen reader does not read any information

### VML component :  v:roundrect with Alt

We reproduce the same thing, but add an Alt attribute on the v:fill element

```
<!--[if mso]>
  <v:roundrect>
    <v:fill src="https://picsum.photos/670/400" alt="alt on vml" type="frame"/>
  </v:roundrect>
<![endif]-->
```

Outlook keeps all VML code in a conditional comment and automatically adds an ID to it, like this :

```
<!--[if gte vml 1]>
  <v:roundrect id="_x0000_s1031">
    <v:fill alt="alt on vml" src="https://picsum.photos/670/400" type="frame"/>
  </v:roundrect>
<![endif]-->
```

Apart from conditional comments, Outlook creates an img tag with a v:shape attribute linked to the VML element ID. The alt on the v:fill is preserved in the commented code but is not carried over to the HTML img tag:

```
<!--[if !vml]-->
  <img width="335" height="201" src="file:////msohtmlclip1/01/clip_image003.png" v:shapes="_x0000_s1031">
<!--[endif]-->
```
So in a case where you have two versions of the same image, the HTML version will be well recognized by screen readers for all other mail clients, but on Outlook, the screen reader will not read any information about the image

## VML component :  v:shape
### VML component :  v:shape without Alt

Here we use the VML shape element to give a particular shape to an image for example.

```
<!--[if mso]>
  <v:shape>
    <v:fill type="frame" src="https://picsum.photos/350/300"/>
  </v:shape>
<![endif]-->
```

If you insert an image into a shape element without Alt, the screen reader does not read anything or passes over it saying "empty"

### VML component :  v:shape with Alt

We reproduce the same thing, but add an Alt attribute on the v:fill element

```
<!--[if mso]>
  <v:shape>
    <v:fill alt="alt on shape image" type="frame" src="https://picsum.photos/350/300"/>
  </v:shape>
<![endif]-->
```

  
Outlook preserves the VML code in a conditional comment and adds an id to the vml element, like this :

```
<!--[if gte vml 1]>
  <v:shape id="_x0000_s1029">
    <v:fill alt="alt on shape image" src="https://picsum.photos/350/300" type="frame"/>
  </v:shape>
<![endif]--> 
```

Apart from conditional comments, Outlook creates an img tag with a v:shape attribute linked to the VML element ID. The Alt on the v:fill is preserved in the commented code but is not carried over to the HTML img tag created

```
<!--[if !vml]-->
  <img width="335" height="201" src="file:////msohtmlclip1/01/clip_image003.png" v:shapes="_x0000_s1031">
<!--[endif]-->
```

Again, on Outlook, the screen reader will not read anything

## VML component :  v:roundrect
### VML component :  v:roundrect without Alt

Here we use the VML around an image to force the rounded shape on Outlook

```
<!--[if mso]>
  <v:roundrect>
<![endif]-->
  <!--[if !mso]><!-->
    <img alt="" src="https://picsum.photos/100/100">
  <!--<![endif]-->
<!--[if mso]>
  </v:roundrect>
<![endif]-->
```

Even if we add an Alt attribute in the HTML part, in Outlook code, this attribute is not found anywhere, it is purely erased. The screen reader therefore passes over the image but does not read any information, or simply says "empty". So the Alt in the html part will be read by all mail clients, but on Outlook, the screen reader will not read anything

### VML component :  v:roundrect with Alt

Same thing here, but we add an Alt Attribute to the VML.

```
<!--[if mso]>
  <v:roundrect alt="this is an image">
<![endif]-->
  <!--[if !mso]><!-->
    <img alt="" src="https://picsum.photos/100/100">
  <!--<![endif]-->
<!--[if mso]>
  </v:roundrect>
<![endif]-->
```

The Alt on the VML v:roundrect element is kept, and is repeated on the html img tag created

```
<!--[if gte vml 1]>
  <v:roundrect id="_x0000_s1026" alt="this is an image"></v:roundrect>
<![endif]-->
```

```
<!--[if !vml]--><img width="100" height="101" src="file:////msohtmlclip1/01/clip_image008.png" alt="this is an image" v:shapes="_x0000_s1026"><!--[endif]-->
```

So on Outlook the Alt here will be well read by the screen reader.

## VML component :  v:rect
### VML component :  v:rect without Alt

Here we surround content in a VML v:rect block. It is often the bus to create what is called an absolute positioning or "false absolute"

```
<!--[if mso]>
  <v:rect>
  <v:textbox>
<![endif]-->

    <table>
      <tr>
        <td>
          <h1>My title</h1>
          <p>My text</p>
        </td>
      </tr>
    </table>

<!--[if mso]>
  </v:textbox>
  </v:rect>
<![endif]-->
```

As usual Outlook keeps all the VML code in its own conditional comment. But in the image it creates, it automatically takes all the text content and inserts it as an Alt attribute.

```
<!--[if gte vml 1]>
<v:rect id="_x0000_s1026"></v:rect><![endif]-->
<!--[if !vml]-->
<img width="664" height="229" src="file:////msohtmlclip1/01/clip_image001.png" alt="Text Box: My title My text" v:shapes="_x0000_s1026">
<!--[endif]-->
```

On Narrator or NVDA, when you let the screen reader read the email, he reads the information as a simple text, without distinguishing the title from the rest. But if you go up or down to the text using the up or down arrow, it distinguishes the title well, saying "level title...". When navigating with the tab key, the whole element is ignored.


### VML component :  v:rect with Alt


```
<!--[if mso]>
  <v:rect alt="some text">
  <v:textbox>
<![endif]-->

    <table>
      <tr>
        <td>
          <h1>My title</h1>
          <p>My text</p>
        </td>
      </tr>
    </table>

<!--[if mso]>
  </v:textbox>
  </v:rect>
<![endif]-->
```

Outlook keeps the vml and adds a bunch of extra code to it. It then displays an image tag with the Alt attribute that was defined in the v:rect element

```
<!--[if gte vml 1]>
  <v:rect id="_x0000_s1026" alt="some text"></v:rect> 
<![endif]-->
<!--[if !vml]-->
  <img width="664" height="229" src="file:////msohtmlclip1/01/clip_image001.png" alt="some text" v:shapes="_x0000_s1026">
<!--[endif]-->
```

The result here is the same: On Narrator or NVDA, when you let the screen reader read the email, he reads the information as a simple text, without distinguishing the title from the rest. But if you go up or down to the text using the up or down arrow, it distinguishes the title well, saying "level title...". When navigating with the tab key, the whole element is ignored.
