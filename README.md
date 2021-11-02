![KartaView](https://github.com/kartaview/upload-scripts/blob/master/logo-KartaView-light.png)

## KartaView Tools

##### Description
Tools developed by [KartaView](https://kartaview.org/) to help contributors.

##### Requirements
* Python 3.6+
* Dependencies from _requirements.txt_ file.
The dependencies can be installed by running:
```
pip3 install virtualenv

virtualenv -p python3 .

source bin/activate

pip3 install -r requirements.txt
```

## 1. Upload photos to KartaView

##### Description
This script is used to upload sequences from a local directory. The available formats are:
* Sequences taken with the OSC mobile apps
* Exif images
 
##### Usage
```
cd /path_to_scripts/osc_tools

# help
python osc_tools.py -h

# help for upload
python osc_tools.py upload -h

# upload all sequences from ~/OSC_sequences folder
python osc_tools.py upload -p ~/OSC_seqences

```

## 2. Generate Exif info from KV metadata file

##### Description
This script generates GPS Exif info for each image from an KV metadata format file.

##### Usage
```
cd /path_to_scripts

# help
python osc_tools.py -h

# help for Exif generation
python osc_tools.py generate_exif -h

# Exif generation for mobile recorded sequence in ~/OSC_sequences/Sequence1 folder
python osc_tools.py generate_exif -exif_source metadata -p ~/OSC_seqences/Sequence1

# Exif generation for custom geojson + imagery 
python osc_tools.py generate_exif -exif_source custom_geojson -p ~/CustomFolderContainingGeoJsonAndImages
```

<details>
  <summary>Custom geojson required fields example:</summary>
 
 ```javascript
      
 {
         "type":"FeatureCollection",
         "features":[
            {
               "type":"Feature",
               "properties":{
                  "order":1.0,
                  "path":"relative_image_path_1.jpg",
                  "direction":236.0,
                  "Lat":1.910309,
                  "Lon":1.503069,
                  "Timestamp":"2020-01-20T08:00:01Z"
               },
               "geometry":{ 
                  "type":"Point",
                  "coordinates":[ 1.503069408072847, 1.910308570011793 ]
               }
            },
            {
               "type":"Feature",
               "properties":{
                  "order":2.0,
                  "path":"relative_image_path_2.jpg",
                  "direction":236.0,
                  "Lat":1.910199,
                  "Lon":1.502908,
                  "Timestamp":"2020-01-20T08:01:21Z"
               },
               "geometry":{
                  "type":"Point",
                  "coordinates":[ 1.502907515952158, 1.910198963742701 ]
               }
            },
            {
               "type":"Feature",
               "properties":{
                  "order":3.0,
                  "path":"relative_image_path_3.jpg",
                  "direction":236.0,
                  "Lat":1.910096,
                  "Lon":1.502764,
                  "Timestamp":"2020-01-20T08:12:10Z"
               },
               "geometry":{
                  "type":"Point",
                  "coordinates":[ 1.50276400212099, 1.910095961756973 ]
               }
            }
         ]
      
 }


   ```
  
</details>


##### Docker
To run the scripts inside a Docker container:
```
make docker
docker run -Pit osc-up osc_tools.py
docker run -Pit --mount type=bind,source="$(pwd)",target=/opt/osc osc-up /opt/osc/osc_tools.py
```
The 'images' directory in the repo will be available in the container at /opt/osc/images
