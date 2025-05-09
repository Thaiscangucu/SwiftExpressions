# Swift Expression
This app analyses the feeling from the user's photo using a trained machine learning image classification model and gives a Taylor Swift song and lyrics according to that feeling.

## ContentView.swift
This file is the main page when the apps opens. It has a NaviagtionStack with a ZStack with a maroon background, a Text with the title, a rectangle button start.

## ResultPage.swift
This is the screen with the results where there is the feeling, the user's photo, the song and the lyrics inside a scroll view. We check the label given by the trained model and compares with the different types of songs, extracted from a cvs file with all the songs and the lyrics.

## Songs.swift
This file contains all the songs and each lyrics in dictionaries separeted by feeling.

## CoreMLViewModel.swift
This file is responsible for using the trained model and visually representing the results. It uses 3 important libraries such as SwiftUI, CoreML and Vision. 
```
import CoreML
import Vision
import SwiftUI
```
In a few words it's a class with one function that returns a string as the result of the trained model. 
The function checkImage first converts the UIImage to a CIImage, then savees the model's configurations in a variable called config and tries to create the model in the code with VNCoreMlModel() with the name of the model and the config just saved.
```
func checkImage(_ image: UIImage) -> String {
        guard let ciImage = CIImage(image: image) else {
            print("Could not convert UIImage to CIImage.")
            exit(0)
        }
        
        var classificationLabel: String = ""
        
        do {
            let config = MLModelConfiguration()
            let model = try VNCoreMLModel(for: FacialExpressions(configuration: config).model)
        
```
After that creates a request using VNCoreMLRequest() with the trained model to extract the results and save it in the varaible results and shows an error message if it fails.
```
let request = VNCoreMLRequest(model: model) { request, error in
                if let results = request.results as? [VNClassificationObservation] {
                    classificationLabel = results.first!.identifier
                } else {
                    print("Invalid Classify")
                }
            }
```
And finally there is a variable handler that gets the information wanted from the image using the request and returns the classification label with the result. 

```
let handler = VNImageRequestHandler(ciImage: ciImage)
            
            try handler.perform([request])
            
        } catch {
            // something went wrong!
            print("Could not load model: \(error.localizedDescription)")
        }
        return classificationLabel
```

