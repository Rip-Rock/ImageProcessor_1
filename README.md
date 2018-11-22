@@ -0,0 +1,218 @@
//: Playground - noun: a place where people can play

import UIKit

let image = UIImage(named: "sample.png")!

// Process the image!

var myRGBA = RGBAImage(image: image)!

let x = 10
let y = 10

let index = y * myRGBA.width + x

var pixel = myRGBA.pixels[index]

pixel.red
pixel.blue
pixel.green

pixel.red = 255
pixel.blue = 0
pixel.green = 0

myRGBA.pixels[index] = pixel

//let newImage = myRGBA.toUIImage()

var totalRed = 0
var totalBlue = 0
var totalGreen = 0

/*
let count = myRGBA.width * myRGBA.height
let avgRed = totalRed/count
let avgGreen = totalGreen/count
let avgBlue = totalBlue/count
*/

/*
 for y in 0..<myRGBA.height {
    for x in 0..<myRGBA.width {
        let index = y * myRGBA.width + x
        var pixel = myRGBA.pixels[index]
        let colorDiff = Int(pixel.red) - avgRed
        if (colorDiff>0)
        {
        pixel.red = UInt8( max(0,min(255,avgRed+colorDiff/effect)))
        myRGBA.pixels[index] = pixel
        }
    }
 }
 */
let avgRed = 119
let avgGreen = 98
let avgBlue = 83
////////

class SomeFilters {
    var image: RGBAImage
    
    init(image: UIImage) {
        self.image = RGBAImage(image: image)!
    }
    
    // Green color Filter
    func Green(value: UInt8 = 0) {
        for a in 0..<self.image.width {
            for b in 0..<self.image.width {
                let index = a * self.image.width + b
                var pixel = self.image.pixels[index]
                let redDiff = Int(pixel.red) - avgRed
                if(redDiff>0) {
                    pixel.red = UInt8(max(0, min(255, avgRed+redDiff/3)))
                }
                self.image.pixels[index]=pixel
            }
        }
    }
    
    // Red color Filter
    func Red(value: UInt8 = 0) {
        for a in 0..<self.image.width {
            for b in 0..<self.image.width {
                let index = a * self.image.width + b
                var pixel = self.image.pixels[index]
                let greenDiff = Int(pixel.green) - avgGreen
                if(greenDiff>0) {
                    pixel.green = UInt8(max(0, min(255, avgGreen+greenDiff/5)))
                }
                self.image.pixels[index]=pixel
            }
        }
    }
    
    // Blue color Filter
    func Blue(value: UInt8 = 0) {
        for a in 0..<self.image.width {
            for b in 0..<self.image.width {
                let index = a * self.image.width + b
                var pixel = self.image.pixels[index]
                let blueDiff = Int(pixel.blue) - avgBlue
                if(blueDiff<0) {
                    pixel.blue = UInt8(max(0, min(255, avgBlue-blueDiff*3)))
                }
                self.image.pixels[index]=pixel
            }
        }
    }
    
    // Yellow color Filter
    func Yellow(value: UInt8 = 0) {
        for a in 0..<self.image.width {
            for b in 0..<self.image.width {
                let index = a * self.image.width + b
                var pixel = self.image.pixels[index]
                let blueDiff = Int(pixel.blue) - avgBlue
                if(blueDiff>0) {
                    pixel.blue = UInt8(max(0, min(255, avgBlue-blueDiff*3)))
                }
                self.image.pixels[index]=pixel
            }
        }
    }
    
    //Brightness Filter
    func DecreaseBrightness(value: UInt8=0) {
        for a in 0..<self.image.height {
            for b in 0..<self.image.width {
                let index = a*self.image.width + b
                var pixel = self.image.pixels[index]
                
              // Change numbers to decrease image brightness
                pixel.red /= 5
                pixel.green /= 5
                pixel.blue /= 5
                
            }
        }
    }
    
    
    func process(filters: [String]) {
        for filter in filters {
            switch filter {
            case "Red":
                self.Red()
            case "Green":
                self.Green()
            case "Blue":
                self.Blue()
            case "Yellow"://///
                self.Yellow()/////
            case "DecreaseBrightness":
                self.DecreaseBrightness()
            default:
                print("Wrong filter; The filter doesn't exist")
            }
        }
    }
    
    func toUIImage() -> UIImage {
        return self.image.toUIImage()!
    }
    
}

let imageProcessing = SomeFilters(image: image)
let filters = ["Yellow"]
imageProcessing.process(filters)
let newImage = imageProcessing.toUIImage()






/*
public class SomeFilters {
    
}
for y in 0..<myRGBA.height {
    for x in 0..<myRGBA.width {
        let index = y * myRGBA.width + x
        var pixel = myRGBA.pixels[index]
        let colorDiff = Int(pixel.red) - avgRed
        if (colorDiff>0)
        {
            pixel.red = UInt8( max(0,min(255,avgRed+colorDiff/effect)))
            myRGBA.pixels[index] = pixel
        }
    }
}

let newImage2 = myRGBA.toUIImage()
image


var effect1 = 10

for y in 0..<myRGBA.height {
    for x in 0..<myRGBA.width {
        let index = y * myRGBA.width + x
        var pixel = myRGBA.pixels[index]
        let colorDiff = Int(pixel.green) - avgGreen
        if (colorDiff>0)
        {
            pixel.green = UInt8( max(0,min(100,avgGreen+colorDiff*effect1)))
            myRGBA.pixels[index] = pixel
        }
    }
}

let newImage3 = myRGBA.toUIImage()
image

*/
