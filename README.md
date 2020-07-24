### Index
- [How to use API](#how-to-use-api)
- [Files Management](#files-management)
	- [How to store video in Content-Based Image Retrieval Database system](#how-to-store-video-in-content-based-image-retrieval-database-system)
	- [How to query a new image](#how-to-query-a-new-image)
- [Files and their meaning](#files-and-their-meaning)


## How to use API

**Posting a video to the server**

```
URL # hosted server URL

POST request -> URL/api/video
request.files['file'] <- should contain video as a file
request.form['category'] <- should contain category name
```

**Quering an Image to the server**

```
URL # hosted server URL

POST request -> URL/api/query

# e.g. request
response = requests.get(URL/api/query, data=open(image.png, 'rb'))

response['category'] <- is the required category (for e.g. jug, teapot, phone or other object name)

```

## Files Management

### How to store video in Content-Based Image Retrieval Database system

```
db = Database()
db.store_video_in_frames(video_file_path, category_name)
db.update_database_with_new_features()
```

What it does?
- Saves the video file
- Breaks it into frames and store in database
- Extracts the feature and saves in the stored-feature compressed file as per VGG model histogram output
- Consider this as **Script ML Model Training on unseen data**

### How to query a new image

```
db = Database()
category = query(image_to_be_queries.jpg, db)

print(category) <- this will print objects name (e.g. jug, teapot, cat)
```

What it does?
- Saves the image
- Takes the stored-features database into the memory
- Queries with the image
- Returns the most likely object's name

### Files and their meaning

- `requirements.txt`: Use it to install python libraries as `pip install -r requirements.txt`
- `run.py`: contains main model for extraction of features and running script
- `webapp.py`: Handles API call and demostrative flask web-app
- `model.py`: Contains main ML VGG model
- `evaluation.py`: Evaluates the query and inferes as per metrics
- `config.py`: Contains all relative paths and configuration
- `videos`: Stores all uploaded videos
- `templates`: templates for web application
- `queryimages`: Saves all images that are queried
- `database`: Contains metadata CSVs and all frames of images and the store-features ML trained model

