# jQuery vs Dojo

There are plenty of places to find comparisons of jQuery and pre – Dojo 1.7 methods but I wanted to have a place to compare jQuery with Dojo’s AMD style.

If you ever find yourself needing to convert a jQuery laden web page to one that uses AMD style Dojo (or vise verse), it helps to have a quick little comparison guide to aid the process. That's what this is. 

Well, that's what it will be - as soon as I actually finish it.
<a id="top"></a>

[Select By Id](#select-by-id)<br>
[Select By Class](#select-by-class)<br>
[Get and Set CSS properties](#css-properties)<br>

## ***Select By Id***
### jQuery
    $(“#idName”);
### Dojo
    Require([“dojo/dom”], function(dom){
        dom.byId(“idName”);
    });

Both methods return the element with id “idName”. Dojo's dom.byId is just an alias for document.getElementById. This means anything you can do with an element retrieved through getElementById you can do with an element accessed through dom.byId.
([Back to top](#top)) <br>

## ***Select By Class***
### *Also select by pseudo class or element*
### jQuery
    //select by class
    $(“.className”);

    //select by element
    $(“div”);

    //select by pseudo Class
    $(“.className:first-child”);

### Dojo
    Require([“dojo/query”], function(query){
        //query by class
        query(“.className”)

        //query by element
        query(“div”)

        //query by pseudo Class
        query(“.className:first-child”)
    });

jQuery’s class selector actually selects all elements with that class so if you chain a method onto the end of the selector, the method will affect every element with that class name by performing an implicit loop.

Dojo’s query, on the other hand, returns a nodeList which you can loop through to access the individual elements in it. However, Dojo's nodeList has some methods attached to it (addClass, style, map, filter...) that will perform the loop automatically.  To change the css of all elements with the class "className" in jQuery you would do this:

    $(".className").css("color", "red");

To do the same thing in Dojo you would do this:

    Require([“dojo/query”, "dojo/dom-style"], function(query){
        query(“.className”).style("color", "red");
        })
    });

As you can see, jQuery abstracts the process making it much simpler while Dojo gives you more control over what you can do with the elements in the nodelist.
([Back to top](#top)) <br>

## ***CSS Properties***
### jQuery
    //Get
    $(“#idName”).css("display")//get the value for a property

    //Set
    $(“#idName”).css("display", "block") //set a single css property
    $(“#idName”).css({"display": "block", "width": "100px"}) //set multiple css properties

### Dojo
    Require([“dojo/dom”, "dojo/dom-style"], function(dom, domStyle){
            //Get
            domStyle.get(dom.byId(“idName”), "display");//get the value for a property

            //Set
            domStyle.set(dom.byId(“idName”), "display", "block");//set a single css property
            domStyle.set(dom.byId(“idName”), {//set multiple css properties
                display: "block",
                width: "100px",
            });
    });
([Back to top](#top)) <br>

