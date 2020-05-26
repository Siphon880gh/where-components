Where Components
===
By Weng Fei Fung. If your website follows a component architecture where there are files named after DOMs, you may get confused when there are too many components, such as which components contains which, which is what, etc. You can copy and paste this code snippet into the console, then run functions to highlight those components in different colors. If the component does not exist, then it can give you a reminder on how to show that component on the website (such as clicking a button to create a new element on the webpage). When moving a mouse over the component, you will also see the component selector in the console as well.

Console snippet
---
```
function whereComponent(selector, colorGroupIndex=0, error="") {
    var colorGroups = [
        "rgba(25,25,25,x)",
        "rgba(125,25,25,x)",
        "rgba(25,125,25,x)",
        "rgba(25,25,125,x)",
        "rgba(225,25,25,x)",
        "rgba(25,225,25,x)"
    ];
    // Parametric Polymorphism
    if(typeof colorGroupIndex==="string") {
        error=colorGroupIndex;
        colorGroupIndex = 0;
    }

    var $el = $(selector);
    colorGroupIndex = Math.abs(colorGroupIndex); // Force value
    colorGroupIndex = colorGroupIndex % colorGroups.length; // Force value
    var colorFaded = colorGroups[colorGroupIndex].replace("x", ".6");
    var colorRegular = colorGroups[colorGroupIndex].replace("x", "1");

    if($el.first().length) {
        $el.css("background-color", colorFaded);
        $el.css("border", `1px solid ${colorRegular}`);
        $el.on("mouseover", (event)=>{
            event.preventDefault();
            event.stopPropagation();
            console.log(`%cComponent: ${selector}`, `background-color:${colorFaded}; color:${colorRegular}; padding:5px;`, $el);
        })
    } else {
        if(error.length)
            console.error(`Cannot find ${selector}. ${error}`);
        else
            console.error(`Cannot find ${selector}. Component does not exist. You may need to interact this app to create some GUI's.`)
    }

} // whereComponent
```

Console highlighting
```
whereComponent(".indicator-current-group-completed", 0, "Not found. Make sure to create a collection, then a habit.");
whereComponent(".habit", 1, "Not found. Make sure to create a collection, then a habit.");
whereComponent(".category", 2, "Not found. Make sure to create a collection.");
whereComponent(".log", 3, "Not found. Make sure to create a collection, then a habit, then add a log.");
```

That's it!