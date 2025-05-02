# SDAVAssetExportSession: Advanced iOS Media Transcoding Library

## Project Overview

SDAVAssetExportSession is a powerful, flexible drop-in replacement for `AVAssetExportSession` designed to simplify video and audio asset transcoding in iOS applications. 

### Key Features
- Full customization of audio and video encoding settings
- Simplified transcoding of media assets
- Asynchronous export with detailed progress tracking
- Supports complex video and audio transformations

### Problem Solved
Developers often struggle with the limitations of Apple's default `AVAssetExportSession`, which provides only a restricted set of preset configurations. This library solves that problem by offering granular control over video and audio encoding parameters.

### Benefits
- Eliminates the complexity of manually configuring `AVAssetWriter` and `AVAssetReader`
- Provides an intuitive API for media asset conversion
- Enables precise control over output video and audio quality
- Supports a wide range of encoding scenarios, from simple conversions to advanced media transformations

The library allows developers to easily specify custom settings for video codec, resolution, bitrate, audio channels, sample rate, and more, making media processing more flexible and tailored to specific application requirements.

## Getting Started, Installation, and Setup

### Prerequisites

- iOS 6.0 or later
- Xcode
- ARC (Automatic Reference Counting) enabled

### Installation

#### CocoaPods

Add the following to your `Podfile`:

```ruby
pod 'SDAVAssetExportSession'
```

Then run:

```bash
pod install
```

#### Manual Installation

1. Clone the repository
2. Copy `SDAVAssetExportSession.h` and `SDAVAssetExportSession.m` into your project
3. Ensure the files are added to your project's target

### Quick Start

```objective-c
// Create an export session with your asset
SDAVAssetExportSession *encoder = [SDAVAssetExportSession.alloc initWithAsset:anAsset];

// Configure output settings
encoder.outputFileType = AVFileTypeMPEG4;
encoder.outputURL = outputFileURL;

// Set custom video settings
encoder.videoSettings = @{
    AVVideoCodecKey: AVVideoCodecH264,
    AVVideoWidthKey: @1920,
    AVVideoHeightKey: @1080,
    AVVideoCompressionPropertiesKey: @{
        AVVideoAverageBitRateKey: @6000000,
        AVVideoProfileLevelKey: AVVideoProfileLevelH264High40,
    },
};

// Set custom audio settings
encoder.audioSettings = @{
    AVFormatIDKey: @(kAudioFormatMPEG4AAC),
    AVNumberOfChannelsKey: @2,
    AVSampleRateKey: @44100,
    AVEncoderBitRateKey: @128000,
};

// Export the video
[encoder exportAsynchronouslyWithCompletionHandler:^{
    if (encoder.status == AVAssetExportSessionStatusCompleted) {
        NSLog(@"Video export succeeded");
    } else if (encoder.status == AVAssetExportSessionStatusCancelled) {
        NSLog(@"Video export cancelled");
    } else {
        NSLog(@"Video export failed with error: %@ (%d)", encoder.error.localizedDescription, encoder.error.code);
    }
}];
```

### Configuration Options

- `outputFileType`: Specify the output file format (e.g., `AVFileTypeMPEG4`)
- `outputURL`: Define the destination file URL for the exported asset
- `videoSettings`: Customize video encoding parameters
- `audioSettings`: Customize audio encoding parameters

### Supported Platforms

- iOS 6.0 and later
- Supports all iOS devices

## Project Structure

The project is a lightweight Objective-C library for video and audio export, primarily consisting of a single custom class `SDAVAssetExportSession`. The repository contains the following key files:

#### Source Files
- `SDAVAssetExportSession.h`: Header file defining the interface for the custom export session class
- `SDAVAssetExportSession.m`: Implementation of the export session functionality
- `SDAVAssetExportSession.podspec`: CocoaPods specification file for library distribution

#### Metadata and Legal Files
- `LICENSE`: Contains the MIT license text for the project
- `README.md`: Project documentation and usage instructions
- `.gitignore`: Specifies intentionally untracked files to ignore

#### Key Components
The library provides a flexible drop-in replacement for `AVAssetExportSession`, offering granular control over audio and video export settings. The primary class `SDAVAssetExportSession` allows developers to customize video and audio encoding parameters beyond the default presets provided by Apple's `AVAssetExportSession`.

## Technologies Used

#### Languages
- Objective-C

#### Frameworks
- Foundation
- AVFoundation

#### Core Technologies
- iOS SDK (minimum version 6.0)
- AVAsset Processing
- Video and Audio Encoding/Transcoding

#### Key Libraries and Components
- AVAssetReader
- AVAssetWriter
- AVVideoComposition
- AVAudioMix

#### Development Tools
- CocoaPods (as evidenced by the .podspec file)

#### Supported Platforms
- iOS (version 6.0 and above)

## Additional Notes

### Performance Considerations

When using `SDAVAssetExportSession`, keep in mind that video and audio transcoding can be computationally intensive. The library provides granular control over encoding settings, which allows for optimizing performance and output quality.

### Encoding Flexibility

The library allows for extensive customization of video and audio encoding parameters:
- Specify custom video codecs, resolution, and bitrate
- Configure audio channel count, sample rate, and encoding format
- Support for partial asset export using `timeRange` property

### Network Optimization

The `shouldOptimizeForNetworkUse` property enables preparing the output file for streaming, which can improve playback performance on networks with varying bandwidth.

### Error Handling

The export process provides detailed error information through the `error` property. Always check the export session's status and error details in the completion handler to handle potential issues gracefully.

### Delegate Methods

For advanced use cases, implement the `SDAVAssetExportSessionDelegate` protocol to gain more control over frame rendering during the export process.

### Compatibility

Designed as a drop-in replacement for `AVAssetExportSession`, compatible with iOS media processing workflows that require fine-grained control over asset export.

## Contributing

We welcome contributions to SDAVAssetExportSession! By contributing, you help improve this library for the entire community.

### Ways to Contribute

- Report bugs by opening GitHub issues
- Suggest features or improvements
- Submit pull requests with bug fixes or enhancements

### Contribution Process

1. Fork the repository
2. Create a new branch for your feature or bugfix
3. Write clean, well-documented code
4. Ensure all existing functionality remains intact
5. Add tests for new features or bug fixes
6. Submit a pull request with a clear description of your changes

### Code Guidelines

- Follow the existing Objective-C code style in the project
- Maintain clear and concise code
- Include comments for complex logic
- Ensure compatibility with the existing implementation

### Reporting Issues

When reporting issues, please include:
- Detailed description of the problem
- Steps to reproduce
- Expected vs. actual behavior
- Relevant environment details (Xcode version, iOS version, etc.)

### Pull Request Process

- Provide a clear and descriptive title for your pull request
- Describe the motivation and context of your changes
- Reference any related issues
- Ensure all CI checks pass before requesting a review

### License

By contributing, you agree that your contributions will be licensed under the MIT License, which matches the project's existing licensing.

## License

This project is licensed under the MIT License. 

#### License Details
The MIT License is a permissive free software license that allows you to:
- Use the software commercially
- Modify the software
- Distribute the software
- Privately use the software

#### Conditions
- Include the original copyright notice
- Include the license text when distributing

#### Warranty
The software is provided "as is" without any warranty.

See the [LICENSE](LICENSE) file for the full license text.

#### Copyright
Copyright (c) 2013 Olivier Poitrey