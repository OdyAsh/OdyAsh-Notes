
Suppose you have this image as viewed in Windows File Explorer:
![[Attachments - Understanding Images Viewed In Windows And In Python/Pasted image 20230310090431.png]]
Also, you know that this image has EXIF metadata, such that orientation key (i.e., 274) is set to 6, which means that, when viewing this image from an editing software (or in our case, python's **pillow** library), then it should be rotated 90 degrees clockwise (CW). Here's a full map of different orientation values to illustrate this ([source](https://sirv.com/help/articles/rotate-photos-to-be-upright/#:~:text=EXIF%20orientation%20values,-The%208%20EXIF&text=%3D%200%20degrees%2C%20mirrored%3A%20image,image%20is%20on%20its%20side.)):
![[Attachments - Understanding Images Viewed In Windows And In Python/Pasted image 20230310090746.png]]
![[Attachments - Understanding Images Viewed In Windows And In Python/Pasted image 20230310090923.png|500]]

However, as you've seen above, <mark style="background: #D2B3FFA6;">windows honors EXIF orientation tag</mark>, which could make you think that these images are fine:

![[Attachments - Understanding Images Viewed In Windows And In Python/Pasted image 20230310091037.png|725]]

When in reality, **all of them have an orientation value of 6 and will be rotated when processed in python**, <mark style="background: #D2B3FFA6;">as pillow does not auto-rotate images.</mark>  ([source](https://github.com/python-pillow/Pillow/issues/4703))
proof:
```python
img_path = './dataset/81. academicPhotos/20191028_210237.jpg' # ememes0001943
img_thumbnail = Image.open(img_path)
img_thumbnail.show()
```
when image is shown:
![[Attachments - Understanding Images Viewed In Windows And In Python/Pasted image 20230310094717.png|350]]

However, if add write the following code:
```python
img_thumbnail = ImageOps.exif_transpose(img_thumbnail)
img_thumbnail.show()
```
It will show correctly:
![[Attachments - Understanding Images Viewed In Windows And In Python/Pasted image 20230310094816.png|250]]

You can even verify this with JPEG Lossless Rotator Program:
![[Attachments - Understanding Images Viewed In Windows And In Python/Pasted image 20230310094843.png|400]]

Ok, so what to do?
You have two options:
1. If you're see that all images in your image folder (windows file explorer) are fine and don't need orienting, then tell python's pillow to transpose the image based on the orientation value, which is automatically done using the `ImageOps.exif_transpose()` function, but take care that <mark style="background: #FF5582A6;">when that function returns a Pillow Image object, its EXIF metadata will not include an orientation value</mark>, which is what we want:

![[Attachments - Understanding Images Viewed In Windows And In Python/Pasted image 20230310100312.png|200]]


2. if most of the images appear in windows file explorer as rotated, then they're probably taken correctly, but <mark style="background: #D2B3FFA6;">the mobile phone's accelerometer probably acted funny such that a wrong orientation tag was applied</mark> ([source](https://superuser.com/questions/975288/why-arent-images-rotated-in-windows-photo-viewer#:~:text=own%20question.%20%E2%80%9C%E2%80%A6-,the%20%22landscape%22%20orientation%20is%20photographically%20correct%2C%20though%20the%20camera%20may%20have%20been%20in%20a%20funny%20position%20causing%20an%20accelerometer%20to%20think%20that%20a%20%22portrait%22%20orientation%20was%20intended,-.%E2%80%9D%20Windows%20Photo)). In that case, it is better to change the orientation value to become 1 (i.e., normal):
   
``` python
directory = "./dataset/81. academicPhotos/"
for filename in os.listdir(directory):
    img = Image.open(os.path.join(directory, filename))
    exif_data = img.getexif()
    if 271 in exif_data.keys() and "samsung" in exif_data[271]:
        orientation = exif_data.get(274)
        if orientation == 6: 
            img.show()
            # img = img.rotate(270, expand=True)
            # img.show()
            exif_data.update([(274, 1)])
            img.save(os.path.join(directory, filename), exif=exif_data)
            break
```

You might want to change `filename` in `img.save()` to be `000.jpg` until you're sure that the adjustments you're making are correct. also, the `and "samsung" in exif_data[271]` part can be omitted 
Side note: `exif_data.update([(274, 1)])` will not automatically rotate, it just change the value from 6 to 1



