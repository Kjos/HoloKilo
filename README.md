# HoloKilo
HoloKilo Positional Tracker for Android, created by Kaj Toet

The HoloKilo positional tracker uses (retro)reflective material for markers. To find the markers, the flash next to the camera is activated and the markers will lit up on the camera’s resulting image. However, to exclude lamps and other bright sources of light, the flash is turned off at intervals to find out which lightpoints are lit up by reflectivity and which are not.

##Requirements
- Android 4+ device (possibly before 4; untested)
- Camera with flash
- Gyroscope, accelerometer and magnetometer
- OpenGL ES 2
- A green circular patch of reflective material (blue and red optional), available at local stores

##Media
Video with latest version:

[![Video 0](http://img.youtube.com/vi/EGo1DYRHhnM/0.jpg)](http://www.youtube.com/watch?v=EGo1DYRHhnM)

Older videos:

[![Video 1](http://img.youtube.com/vi/K6ztsdTKuzc/0.jpg)](http://www.youtube.com/watch?v=K6ztsdTKuzc)
[![Video 2](http://img.youtube.com/vi/VQW2xLNd_-Y/0.jpg)](http://www.youtube.com/watch?v=VQW2xLNd_-Y)
[![Video 3](http://img.youtube.com/vi/ydd2h-7mcxk/0.jpg)](http://www.youtube.com/watch?v=ydd2h-7mcxk)

Note: Videos on the right are taken with a Moto G 2nd phone, which is known for its bad gyroscope. The screenrecorder also take away a lot of the smoothness, due to a performance impact. Real life performance is a consistent 30fps on the Moto G 2nd.
Also, videos were taken of an older version than the one on this Github and I've improved latency considerably.

##Possible usecases
- Virtual Reality (VR)
- Augmented Reality (AR)
- Robotics
- Drones
- More..!

##Notes
The Unity implementation seems to have more latency than the Java implementation. This may be due to the fact that I used JavaAndroidObject to communicate with the Java side, which could cause problems due to caching.

There needs to be done some more research on different light conditions. In my testing the exposure lock needs to be on at night and set to minimal exposure in daylight.

Distance calculation happens by the blob size (roughly put). It might be better to use three blobs in a triangle and calculate the distance that way. In an earlier version I also calculated the rotation with Coplanar Posit, but I figured it to be not worth the effort pursueing.

Calculating distance by blob size has some disadvantages due to camera movement causing smear of the blobs. I try to counter this with the gyroscope (more movement is smaller actual blob), but it needs some tweaking.

Currently 3 blobs are tracked (green for camera viewmatrix, red and blue extra for example for controllers), but it is very easy to change this. The blobfinder doesn't need to perform much more work for more blobs.

Some have concerns over the battery drain and heat from the camera flash. In my testing this wasn't a problem at all. If I understand correctly, the average flash led consumes 80-100 mA and the average battery has 2000mAh. With that in mind the average phone can power the flash 20 hours not taking in other factors such as the display. I also have not noticed my flash degrading, but this could be the case with presumably older phones. Given that Android provides its own flashlight function in the newer versions, I don't think there is a problem with it.

Different (retro) reflective materials have different properties. I have found the 'car neon reflective tape' from aliexpress to be good for close by. Some other reflective material I ordered from a local webshop, shiny looking with diamond patterns, works better for me for tracking at larger distances (which is shown in the videos), but sometimes less closeby. Don't spend too much on the materials; it should work with cheap materials of a few bucks!

Some examples: 

long range:
http://www.aliexpress.com/item/5Meter-Green-Reflective-Film-Self-adhesive-PET-Tape-Reflective-Tape-Sticker-For-Truck-Car-Motorcycle-Warning/32602596833.html

short range:
http://www.aliexpress.com/item/5cmx10M-Reflective-Strips-Car-Stickers-for-car-styling-Motorcycle-decoration-Automobiles-Safety-Warning-Mark-Tape-Green/32622350483.html

I've used colored materials because they're easy to distinguish from for example a metallic vase or mirror, which can also reflect light as if retro reflective. Besides that, lamps tend to be white and it is preferable to filter them out. 
I've also done testing with a colored (green) filter in front of the flash and using regular white reflective material; this works too.

##Example
https://github.com/Kjos/HoloKilo/raw/master/holokilo-debug.apk

It tracks a circular green (retro) reflective marker. I use a marker of about 10cm in diameter.
