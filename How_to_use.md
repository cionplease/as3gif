# Basic Usage #

## The GIFPlayer ##

The GIFPlayer class is used to play the gif animation.

It can load gif file from an URLRequest object or a ByteArray object.

Example:
```
package 
{
	import flash.display.Sprite;
	import flash.net.URLRequest;
	import org.gif.player.GIFPlayer;
	
	public class Main extends Sprite
	{
		public function Main():void
		{
			var request:URLRequest = new URLRequest("diego.gif");
			
			var player:GIFPlayer = new GIFPlayer();
			player.load(request);
			
			addChild(player);
		}
	}
}
```

## The GIFEncoder ##
The GIFEncoder class use to create a gif file by frames.

Example(draw two frames and add to GIFEncoder then play the gif data by GIFPlayer):

```
package 
{
	import flash.display.BitmapData;
	import flash.display.Shape;
	import flash.display.Sprite;
	import flash.utils.ByteArray;
	import org.gif.encoder.GIFEncoder;
	import org.gif.player.GIFPlayer;
	
	public class Main extends Sprite
	{
		public function Main():void
		{
			var frames:Array = createFrames();
			
			var encoder:GIFEncoder = new GIFEncoder();
			
			encoder.setRepeat(0);			//AUTO LOOP
			encoder.setDelay(500);
			
			encoder.start();			//MUST HAVE!
			
			encoder.addFrame(frames[0]);
			encoder.addFrame(frames[1]);
			
			encoder.finish();			//MUST HAVE!
			
			playGIF(encoder.stream);
		}
		
		private function playGIF(data:ByteArray):void
		{
			data.position = 0;
			
			var player:GIFPlayer = new GIFPlayer();
			player.loadBytes(data);
			
			addChild(player);
		}
		
		private function createFrames():Array
		{
			var shape:Shape = new Shape();
			shape.graphics.lineStyle(1, 0);
			
			shape.graphics.moveTo(60, 0);
			shape.graphics.lineTo(60, 120);
			
			var frame1:BitmapData = new BitmapData(120, 120);
			frame1.draw(shape);
			
			shape.graphics.clear();
			
			shape.graphics.lineStyle(1, 0);
			shape.graphics.moveTo(0, 60);
			shape.graphics.lineTo(120, 60);
			
			var frame2:BitmapData = new BitmapData(120, 120);
			frame2.draw(shape);
			
			return [frame1, frame2];
		}
	}
}
```