import 'package:flutter/material.dart';

void main() {
  runApp(PhotoGalleryApp());
}

class PhotoGalleryApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Photo Gallery',
      theme: ThemeData(
        primarySwatch: Colors.green,
      ),
      home: PhotoGalleryScreen(),
    );
  }
}

class PhotoGalleryScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Photo Gallery'),
      ),
      body: SingleChildScrollView(
        child: Column(
          children: [
            Container(
              margin: EdgeInsets.all(16.0),
              child: Text(
                'Welcome to My Photo Gallery!',
                style: TextStyle(
                  fontSize: 24.0,
                  fontWeight: FontWeight.bold,
                ),
              ),
            ),
            Container(
              margin: EdgeInsets.all(16.0),
              child: TextField(
                decoration: InputDecoration(
                  hintText: 'Search photos',
                  border: OutlineInputBorder(),
                  contentPadding: EdgeInsets.symmetric(
                    vertical: 12.0,
                    horizontal: 16.0,
                  ),
                ),
              ),
            ),
            Wrap(
              spacing: 8.0,
              runSpacing: 8.0,
              children: [
                buildPhotoButton(context, 'https://cdn.pixabay.com/photo/2017/02/20/18/03/cat-2083492_1280.jpg', 'caption'),
                buildPhotoButton(context, 'https://cdn.pixabay.com/photo/2017/07/25/01/22/cat-2536662_1280.jpg', 'caption'),
                buildPhotoButton(context, 'https://cdn.pixabay.com/photo/2016/09/05/21/37/cat-1647775_1280.jpg', 'caption'),
                buildPhotoButton(context, 'https://cdn.pixabay.com/photo/2017/11/09/21/41/cat-2934720_1280.jpg', 'caption'),
                buildPhotoButton(context, 'https://cdn.pixabay.com/photo/2016/03/28/10/05/kitten-1285341_1280.jpg','caption'),
                buildPhotoButton(context, 'https://cdn.pixabay.com/photo/2016/09/07/16/19/pile-1651945_1280.jpg', 'caption'),
              ],
            ),
            ListView(
              shrinkWrap: true,
              children: [
                ListView.builder(
                  shrinkWrap: true,
                  physics: NeverScrollableScrollPhysics(),
                  itemCount: 3,
                  itemBuilder: (context, index) {
                    final photoIndex = index + 1; // Start index from 1
                    return ListTile(
                      leading: Image.network(
                        'https://cdn.pixabay.com/photo/2017/09/01/00/15/png-2702691_1280.png',
                        fit: BoxFit.fitHeight,
                      ),
                      title: Text('Photo $photoIndex'),
                      subtitle: Text('Category $photoIndex'),
                    );
                  },
                )
              ],
            ),
          ],
        ),
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: () {
          final snackBar = SnackBar(
            content: Text('Photos Uploaded Successfully!'),
          );
          ScaffoldMessenger.of(context).showSnackBar(snackBar);
        },
        child: Icon(Icons.cloud_upload),
      ),
    );
  }

  Widget buildPhotoButton(BuildContext context, String imageUrl, String caption) {
    return ElevatedButton(
      onPressed: () {
        final snackBar = SnackBar(
          content: Text('Clicked on photo!'),
        );
        ScaffoldMessenger.of(context).showSnackBar(snackBar);
      },
      style: ElevatedButton.styleFrom(
        padding: EdgeInsets.zero,
      ),
      child: Column(
        children: [
          Image.network(
            imageUrl,
            width: 120.0,
            height: 120.0,
            fit: BoxFit.cover,
          ),
          SizedBox(height: 8.0),
          Text(caption),
        ],
      ),
    );
  }
}
