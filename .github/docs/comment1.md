**Proposal**

**Root Cause**

React native image caching doesn't work the same way in iOS like android/web. Image has an extra param(cache) for iOS to specify caching logic specific to iOS. We need to add 'force-cache' as the param value to reuse the cached image which it doesn't do by default like android.

**References**

https://reactnative.dev/docs/image#source
https://reactnative.dev/docs/image#imagecacheenum-ios

**Code change**
```
--- a/src/components/Avatar.js
+++ b/src/components/Avatar.js
@@ -94,7 +94,7 @@ class Avatar extends PureComponent {
                     )
                     : (
                         <Image
-                            source={{uri: this.props.source}}
+                            source={{uri: this.props.source, cache: 'force-cache'}}
                             defaultSource={getAvatarDefaultSource(this.props.source)}
                             style={imageStyle}
                             onError={() => this.setState({imageError: true})}
```


testinf
