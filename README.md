# stylegan experiment
playing around with styleGAN with my own images to futher understanding

## background
I wanted to see if I can use [StyleGAN](https://github.com/NVlabs/stylegan) on my own images instead of human faces with limited computational resources like with a GTXS 1080 TI and limited RAM. I wanted to use images that are quite similar to each other, and I decided to use space related images (stars, planets, moon, etc) because they at least share a similar background which can be significant and impact results if there is significant disparity, and space is cool. 

## process
I needed lots of space related images so I went over to the the [astrophotography subreddit](https://www.reddit.com/r/astrophotography/) and downloaded about 900 images. I filtered out gifs,videos, and images that were obviously not photos of planets or stars (like infographics), and resized all images to 128x128. Then, I used the [dataset_tool.py](https://github.com/NVlabs/stylegan/blob/master/dataset_tool.py) and its `create_from_images` function to convert the images to TFRecords. Inside the [train.py](https://github.com/NVlabs/stylegan/blob/master/train.py) file, I set the number of gpus by uncommenting line 46. I followed the example on line 101 in train.py, where I replaced 'celebahq' with the name of my TFRecord directory. I trained for roughly 48 hours (program was actually killed by kernel most likely due to memory exhaustion) and thus didn't train for the full expected training time of "41 days" (according to StyleGAN repo for single GPU). Before generating images, the file that does it (pretrained_example.py) needs to be changed so that it will use the generator from your images instead of whatever the default is. Instead of the url linking to a google drive file, link the url to the last "network snapshot" in the custom dataset directory inside results, before running it. I ran it several times and got some good results like [this](good_results/example349.png) and [this](good_results/example316.png). I also got many bad results where the generated tried to put stars inside planets and moons like [this](bad_results/example18.png) and [this](bad_results/example105.png). 

Good example:

![image](good_results/example333.png)                               

Bad example:

![image](bad_results/example18.png) 



inspired by similar project done with StyleGAN but with anime girl faces ([link](https://www.gwern.net/Faces)) 

