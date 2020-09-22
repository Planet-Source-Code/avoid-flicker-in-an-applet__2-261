<div align="center">

## Avoid Flicker in an applet


</div>

### Description

The key to fixing flicker is realizing that the screen isn't actually painted in the paint() method. The pixels get put on the screen in the update() method which most applets don't override. However by overriding the update() method you can do all your painting in an offscreen Image and then just copy the final Image onto the screen with no visible flicker.

(Java FAQ:found on the web at:http://sunsite.unc.edu/javafaq/javafaq.html)
 
### More Info
 


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[N/A](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/empty.md)
**Level**          |Unknown
**User Rating**    |5.0 (15 globes from 3 users)
**Compatibility**  |Java \(JDK 1\.1\)
**Category**       |[Graphics](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/graphics__2-75.md)
**World**          |[Java](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/java.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/avoid-flicker-in-an-applet__2-261/archive/master.zip)





### Source Code

```
Add the following three private fields to your applet and the public update() method. Flicker will magically disappear.
 private Image offScreenImage;
 private Dimension offScreenSize;
 private Graphics offScreenGraphics;
 public final synchronized void update (Graphics g) {
  Dimension d = size();
  if((offScreenImage == null) || (d.width != offScreenSize.width) || (d.height != offScreenSize.height)) {
   offScreenImage = createImage(d.width, d.height);
   offScreenSize = d;
   offScreenGraphics = offScreenImage.getGraphics();
  }
  offScreenGraphics.clearRect(0, 0, d.width, d.height);
  paint(offScreenGraphics);
  g.drawImage(offScreenImage, 0, 0, null);
 }
```

