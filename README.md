# metadata

The metadata project extracts metadata from files.

To build a JAR of the project, first make sure Maven is installed, and then, in a command line, change to the root directory of the project, and then type 'mvn package'.

Here is some useful code:

```java
package com.schneider.utils.metadata;

import java.io.File;
import java.io.IOException;

import org.apache.tika.exception.TikaException;
import org.apache.tika.parser.mp3.ID3Tags;
import org.xml.sax.SAXException;

import com.mpatric.mp3agic.InvalidDataException;
import com.mpatric.mp3agic.UnsupportedTagException;
import com.schneider.utils.metadata.audio.Mp3Detector;
import com.schneider.utils.metadata.image.ImageFormat;
import com.schneider.utils.metadata.mimetype.MimeTypeDetector;

/**
 * Hello world!
 *
 */
public class App 
{
    public static void main( String[] args ) throws IOException, SAXException, TikaException, UnsupportedTagException, InvalidDataException
    {
        File file = new File("C:\\Users\\jschneider\\Downloads\\music\\Sufjan Stevens\\The Age of Adz\\01 Futile Devices.mp3");
        Mp3Detector detector = new Mp3Detector();
        ID3Tags tags = detector.parse(file);
        System.out.println("Album: " + tags.getAlbum());
        System.out.println("Artist: " + tags.getArtist());
        System.out.println("Composer: " + tags.getComposer());
        System.out.println("Genre: " + tags.getGenre());
        System.out.println("Tags present: " + tags.getTagsPresent());
        System.out.println("Title: " + tags.getTitle());
        System.out.println("Track Number: " + tags.getTrackNumber());
        System.out.println("Year: " + tags.getYear());
        System.out.println("Comments: " + tags.getComments());

        detector.writeArtwork(file, new File("saved.jpg"), ImageFormat.JPEG);
        detector.writeArtwork(file, new File("saved.png"), ImageFormat.PNG);
        detector.writeArtwork(file, new File("saved.gif"), ImageFormat.GIF);
        detector.writeArtwork(file, new File("saved.bmp"), ImageFormat.BMP);
        
        MimeTypeDetector detector2 = new MimeTypeDetector();
        System.out.println("MIME type: " + detector2.detectMimeType(file));
    }
}
```
