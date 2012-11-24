# GSDropboxActivity

An iOS 6 UIActivity subclass for uploading to Dropbox.

This is currently work in progress. All suggestions gratefully received!

# Usage instructions

## 1. Install the Dropbox iOS SDK

Download the latest [Dropbox iOS SDK][dropbox-ios-sdk] and follow Dropbox's instructions for incorporating it into your app.

**GSDropboxArchive assumes you have configured the shared DBSession object appropriately.** If you follow Dropbox's integration instructions you will have done this. In essence, you just need to make sure you include this in your application delegate's `application:didFinishLaunchingWithOptions:` method:

```objective-c
#import <DropboxSDK/DropboxSDK.h>

...

DBSession* dbSession =
    [[[DBSession alloc]
      initWithAppKey:@"APP_KEY"
      appSecret:@"APP_SECRET"
      root:ACCESS_TYPE] // either kDBRootAppFolder or kDBRootDropbox
     autorelease];
[DBSession setSharedSession:dbSession];
```

## 2. Add GSDropboxActivity to your project

Just copy all the .h, .m and .png files into your Xcode project.

## 3. Add a GSDropboxActivity object to your list of custom activities

```objective-c
- (void)handleShareButton:(id)sender
{
    NSArray *itemsToShare = @[
        // Your items to share go here.
        // GSDropboxActivity can share NSURL objects where each object is
        // the file URL to a file on disk.
    ];
    NSArray *applicationActivities = @[
        [[GSDropboxActivity alloc] init]
    ];
    UIActivityViewController *vc = [[UIActivityViewController alloc] initWithActivityItems:itemsToShare
                                                                     applicationActivities:applicationActivities];

    // Present modally - suitable for iPhone.
    // On iPad, you should present in a UIPopoverController
    [self presentViewController:vc animated:YES completion:NULL];
}
```


# License

[![Creative Commons License][cc-by-30-icon]][cc-by-30]

This work is licensed under a [Creative Commons Attribution 3.0 Unported License][cc-by-30].

You're free to use this code in any project, including commercial. Please include the following text somewhere suitable, e.g. your app's About screen:

**Uses GSDropboxArchive by Simon Whitaker**

[cc-by-30-icon]: http://i.creativecommons.org/l/by/3.0/88x31.png
[cc-by-30]: http://creativecommons.org/licenses/by/3.0/
[dropbox-ios-sdk]: https://www.dropbox.com/developers/reference/sdk