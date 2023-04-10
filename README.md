# Java Swing Webcam Capture and Save

Create Java Swing Project to Capture and Save Webcam Image

## Getting Started

Download and open in Netbean 8.xx IDE
### Prerequisites
* Java SDK 8.xx
* NetBean IDE
* Generic Webcam Java API  http://webcam-capture.sarxos.pl/
* Library required (found in https://github.com/sarxos/webcam-capture)
1) bridj-0.7.0.jar
2) slf4j-api-1.7.2.jar
3) webcam-capture-0.3.13-20180202.082008-3.jar

```

//////////SWING COMPONENT////////////
    private javax.swing.JButton jButton1;
    private javax.swing.JButton jButton2;
    private javax.swing.JPanel jPanel1;
    private javax.swing.JPanel panelCam;

//////////  IMPORT /////////////////////

import com.github.sarxos.webcam.Webcam;
import com.github.sarxos.webcam.WebcamPanel;
import com.github.sarxos.webcam.WebcamResolution;
import java.awt.Dimension;
import java.awt.FlowLayout;
import java.awt.HeadlessException;
import java.io.File;
import java.io.IOException;
import javax.imageio.ImageIO;
import javax.swing.JOptionPane;

/////////// IN MAIN CLASS/////////

public class NewJFrame extends javax.swing.JFrame {
    private final Dimension ds=new Dimension(450,360);
    private final Dimension cs= WebcamResolution.VGA.getSize();
    private final Webcam wCam=Webcam.getDefault();
    private final  WebcamPanel wCamPanel=new WebcamPanel(wCam,ds,false);  
    
////// AFTER INIT COMPONENT ////////////

    public NewJFrame() {
        initComponents();
        wCam.setViewSize(cs);
        wCamPanel.setFillArea(true);
        panelCam.setLayout(new FlowLayout());
        panelCam.add(wCamPanel);      
 }
 
 //////////////// AT CAPTURING EVENT ///////////////// 
 
        Thread t = new Thread(){
        @Override        
        public void run(){
        wCamPanel.start();
    }
    };
    t.setDaemon(true);
    t.start();
    
 /////////////////// SAVING EVENT ///////////
 
  try{
          File file= new File(String.format("capture-%d.jpg",System.currentTimeMillis())) ;
        ImageIO.write(wCam.getImage(), "JPG", file);
        JOptionPane.showMessageDialog(this, "image saved on :\n" + file.getAbsolutePath(),"CamCap",1);
        }
        catch(HeadlessException | IOException e){
            JOptionPane.showMessageDialog(this,"Image Not Saved :/n"+e.getMessage(),"Cam",0);
            
        }
 
```

### Installing

Clone git and open dist folder and run JavaApplication2.jar in windows environment


## Built With

* [sarxos Generic Webcam Java API](https://github.com/sarxos/webcam-capture) - The webcam generic Library
* [Netbeans](https://netbeans.org/downloads/) - Netbeans IDE
* [Java SDK ](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) - as per your OS

## Contributing & Issue

Please read [CONTRIBUTING.md](https://github.com/dodobasu/java_swing_webcam/issues) for details on our code of conduct, and the process for submitting pull requests to us.


## Authors

* **Prativas Basu** - *Initial work* - [Bartosz Firyn](https://github.com/sarxos)


## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details

## Acknowledgments

* Bartosz Firyn
