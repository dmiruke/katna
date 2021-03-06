.. _tutorials_video:

How to Use
==========

Video
------
**Step 1**

Import the video module 

.. code-block:: python

   from Katna.video import Video

**Step 2**

Instantiate the video class inside your main module (necessary for multiprocessing in windows)

.. code-block:: python

     if __name__ == "__main__":
          vd = Video()
   
**Step 3**

Call the **extract_frames_as_images** method.
The method accepts two parameters and returns a list of numpy 2D array which are images. 
Refer to API reference for further details. Below are the two parameters required by the method

1. **no_of_frames**: Number of key frames to be extracted

2. **file_path**: Video file path.


.. code-block:: python

     imgs = vd.extract_frames_as_images(no_of_frames = no_of_frames_to_returned, \
     file_path= video_file_path)


**Step 4 (Optional)**

Incase you want to persist the extracted key frames then call the **save_frame_to_disk** method.
The method accepts three parameters and returns nothing. 
Refer to API reference for further details. Below are the two parameters required by the method

1. **frame**: In-menory images generated by extract_frames_as_images method.

2. **file_name**:  File name pattern for the persisted image.

3. **file_path**: Folder location where files needs to be saved

4. **file_ext**: File extension indicating the file type for example - ‘.jpg’


.. code-block:: python

     vd.save_frame_to_disk(img, file_path=output_folder_video_image, \
          file_name="test_"+str(counter), file_ext=".jpeg")

Code below is a complete example.

.. code-block:: python
   :emphasize-lines: 1,8,11,14,17-18,20-21,27-28
   :linenos:

   from Katna.video import Video
   import os
   
   # For windows, the below if condition is must.
   if __name__ == "__main__":

     #instantiate the video class
     vd = Video()

     #number of key-frame images to be extracted
     no_of_frames_to_returned = 12

     #Input Video file path
     video_file_path = os.path.join(".", "tests","data", "pos_video.mp4")

     #Call the public key-frame extraction method
     imgs = vd.extract_frames_as_images(no_of_frames = no_of_frames_to_returned, \
          file_path= video_file_path)

     # Make folder for saving frames
     output_folder_video_image = 'selectedframes'
     if not os.path.isdir(os.path.join(".", output_folder_video_image)):
          os.mkdir(os.path.join(".", output_folder_video_image))

     # Save all frames to disk
     for counter,img in enumerate(imgs):
          vd.save_frame_to_disk(img, file_path=output_folder_video_image, \
               file_name="test_"+str(counter), file_ext=".jpeg")

