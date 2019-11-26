# Video Frame Analysis Sample

This sample contains a library, along with two applications, for analyzing video frames from a webcam in near-real-time using APIs from [Microsoft Cognitive Services][]. The library and applications are implemented in C#, and use the [OpenCvSharp][] package for webcam support. 

[Microsoft Cognitive Services]: https://www.microsoft.com/cognitive-services
[OpenCvSharp]:                  https://github.com/shimat/opencvsharp

## Getting Started

1. Get API keys for the Vision APIs from [microsoft.com/cognitive][Sign-Up]. For video frame analysis, the applicable APIs are:
    - [Computer Vision API][]
    - [Face API][]
2. Open the sample in Visual Studio 2015, build and run the sample applications:
    - For BasicConsoleSample, the Face API key is hard-coded directly in [BasicConsoleSample/Program.cs](Windows/BasicConsoleSample/Program.cs).
    - For LiveCameraSample, the keys should be entered into the Settings pane of the app. They will be persisted across sessions as user data.
3. Reference the VideoFrameAnalyzer library from your own projects.

[Sign-Up]:             https://www.microsoft.com/cognitive-services/en-us/sign-up
[Computer Vision API]: https://www.microsoft.com/cognitive-services/en-us/computer-vision-api
[Face API]:            https://www.microsoft.com/cognitive-services/en-us/face-api

## Using the VideoFrameAnalyzer Library

You can start using the library with only a few lines of code:
```csharp
// Create Face API Client. 
FaceServiceClient faceClient = new FaceServiceClient("<subscription key>","<api root>");
// Create grabber, with analysis type Face[]. 
FrameGrabber<Face[]> grabber = new FrameGrabber<Face[]>();
// Set up Face API call, which returns a Face[]. Simply encodes image and submits to Face API. 
grabber.AnalysisFunction = async frame => return await faceClient.DetectAsync(frame.Image.ToMemoryStream(".jpg"));
// Tell grabber to call the Face API every 3 seconds. 
grabber.TriggerAnalysisOnInterval(TimeSpan.FromMilliseconds(3000));
// Start running. 
await grabber.StartProcessingCameraAsync();
```


## License

All Microsoft Cognitive Services SDKs and samples are licensed with the MIT License. For more details, see [LICENSE](LICENSE.md).

