A: How to use the GIFPlayer in Flex project?

Q: You just need a UICompent the wrap the player :)
```
var container:UICompent = new UICompent();
var gif:GIFPlayer = new GIFPlayer();
 
//do the wrap
container.addChild(gif);
 
//load the image...
 
//Add the player into your control or the application
the_flex_control_or_application.addChild(container);
```