# Dengue Mobile4D

## Features
### Client-side
1. User: Json request with lat & lng
2. Receive jobs
3. Take & send photos
### Server-side
1. Find nearest points
2. Send missing streets
3. Run detection model / store to DB / update missing streets

## Missing Streets
Overall missing-streets in Nakhon-si-thammarat province
![Missing-streets](doc/missing-streets.png  "Missing Streets")
Left (an available of Google street view images), Right (linestrings of the missing streets)
![Missing-streets](doc/gsv-missing-streets.png  "Missing Streets")

## How to run

* Python Installation
```
pip3 install -r requirements.txt
```

* Initialize server
```
python3 index.py
```
### Test request
* Linux users
```
curl --header "Content-Type: application/json" \
--request POST \
--data '{"send":"okay"}' \
http://localhost:5000/foo

```

* Windows users
```
curl -H "Content-Type: application/json" -X POST http://localhost:5000/foo -d "{\"send\":\"okay\"}"
```

## API Reference

### Request missing streets
Send current location of the users
```json
{
  "type": "Feature",
  "geometry": {
    "type": "Point",
    "coordinates": [99.8, 8.1]
  },
  "properties": {
	"province": "Nakhon Si Thammarat",
	"district": "Phrom Khiri",
	"subdistrict": "Thon Hong"
  }
}
```

### Submit photos
* Sample JSON request (sending images to the server)
```json
curl \
-F "file=@/home/poom/Pictures/1.jpg" \
-F "file=@/home/poom/Pictures/2.jpg"\
 localhost:5000/upload/images/

```

* Sample JSON respond from the server
```json
{
  "message": "The images have been uploaded.", 
  "status": "success"
}

```

* Sample output on the server
```console
ImmutableMultiDict([('file', <FileStorage: '1.jpg' ('image/jpeg')>), ('file', <FileStorage: '2.jpg' ('image/jpeg')>)])
Accept incoming file: 1.jpg
Save it to: static/uploads/7901bcd5-2d5a-4e2e-9e48-de89c4d18e28/1.jpg
Accept incoming file: 2.jpg
Save it to: static/uploads/7901bcd5-2d5a-4e2e-9e48-de89c4d18e28/2.jpg
127.0.0.1 - - [27/Jun/2018 00:04:49] "POST /upload/images/ HTTP/1.1" 200 -

```


