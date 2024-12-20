### **Step 0: Download Required Data**
- Download the Image Magick scripts and place them wherever you plan on performing the spherical pano and cubemap conversions
- Download all remaining tools that are listed at the foot of this README (if needed)
- Download whichever flattened spherical panorama you want to use for this project (the example used can be found at https://polyhaven.com/a/rostock_laage_airport)
- There is 1 image that can't be uploaded to this GitHub repo due to its size. You may obtain it by downloading them from my Google Drive. Please put the "rostock_laage_airport_sightings.png" in the source folder's 6_assembled_modified_cubemap_pics and 7_final_spherical_panorama folders of your cloned local repository. Link to my Google Drive: https://drive.google.com/drive/folders/1DZJpdaJGWz9pK6noSZTLWAl2QY8gazvR?usp=sharing

### **Step 1: Download an Appropriate Flattened Spherical Panorama**
- **Folder**: `1_original_spherical_panorama`
- **Procedure**: Download a high-resolution spherical panorama image (equirectangular projection) with a resolution of 8192x4096 or smaller. Larger images are discouraged as they may take too long to process during conversions.
- **Description**: Contains the original spherical panorama image (JPG) with a resolution of **8192x4096**.
- **Purpose**: Serves as the starting point for the challenge creation.
- **Source**: PolyHaven: HDRIs / Rostock-Laage Airport
![alt text](1_original_spherical_panorama/sources/Source_of_Spherical_Panorama.png)

### **Step 2: Convert to Cubemap Format**
- **Folder**: `2_original_cubemap_pics`
- **Procedure**: Convert the flattened spherical panorama into a cubemap format, producing six individual faces (front, back, left, right, top, bottom) and a montage.
- **Description**: The spherical panorama is converted into six cubemap faces (front, back, left, right, top, bottom).
- **Tools**: Fred's ImageMagick Scripts: sphericalpano2cube script.
- **CLI**:  bash sphericalpano2cube -d 2048 rostock_laage_airport.jpg rostock_laage_airport_cubemapped.jpg
- **Output**: A complete cubemap montage and its 6 individual faces.
![alt text](2_original_cubemap_pics/sources/Downloaded_sphericalpano2cube_Script.png) ![alt text](2_original_cubemap_pics/sources/Source_of_SphericalPano_to_Cubemap_Converter_Script_1.png) ![alt text](2_original_cubemap_pics/sources/Source_of_SphericalPano_to_Cubemap_Converter_Script_2.png)
![alt text](2_original_cubemap_pics/cli_executions/sphericalpano2cube_command.png)

### **Step 3: Generate and Split QR Code**
- **Folder**: `3_chopped_qr`
- **Procedure**: Generate a level L (lowest data recovery level) QR code and split it into four equal parts. These pieces will later be embedded into the cubemap faces.
- **Description**: The QR code is divided into 4 pieces for embedding into specific cubemap faces.
- **Tools**: Canva's QR Code Generator & ImageMagick's convert command.
- **CLI**:  convert ATHACKCTFQHERE_IS_QALDO.png -crop 50%x50% +repage chop-%d.jpg
- **Output**: Each QR code piece will be inserted in a different cubemap face among the 6 produced.
![alt text](3_chopped_qr/cli_executions/image_chop_command.png)

### **Step 4: Transparent QR Code Pieces**
- **Folder**: `4_transparent_white_pixel_qr_chops`
- **Procedure**: Edit the QR code pieces to make all white pixels transparent, increasing the camouflage of the QR code within the cubemap faces.
- **Description**: The white pixels in the QR code pieces are made transparent to camouflage the QR code chops in the cubemap faces.
- **Tools**: GIMP or other image editing software.

### **Step 5: Embed QR Code Pieces into Cubemap Faces**
- **Folder**: `5_redacted_edited_cubemap_pics`: Contains the same images as above, but all metadata (e.g., EXIF) has been stripped during export.
- **Procedure**: Export the edited cubemap faces as JPG files, ensuring all metadata (e.g., EXIF) is stripped.
- **Purpose**: To provide a clean version for the challenge.
- **Tools**: GIMP or other image editing software.

#### **Back**
![alt_text](5_redacted_edited_cubemap_pics//deeper/back/rostock_laage_airport_cubemapped_back.jpg)
- **GIMP**: paste one of the QR codes in rostock_laage_airport_cubemapped_back.jpg
![alt_text](5_redacted_edited_cubemap_pics//deeper/back/rostock_laage_airport_back_edit_redacted.jpg)

#### **Left**
![alt_text](5_redacted_edited_cubemap_pics//deeper/left/rostock_laage_airport_cubemapped_left.jpg)
- **CLI**: bash polar -m polar2rect -r 0,m -v white rostock_laage_airport_cubemapped_left.jpg rostock_laage_airport_cubemapped_left_edit.jpg
![alt_text](5_redacted_edited_cubemap_pics//deeper/cli_executions/polar2rect_left_command.png)
![alt_text](5_redacted_edited_cubemap_pics//deeper/left/rostock_laage_airport_cubemapped_left_edit.jpg)
- **GIMP**: paste one of the QR codes in rostock_laage_airport_cubemapped_left_edit.jpg
![alt_text](5_redacted_edited_cubemap_pics//deeper/left/rostock_laage_airport_cubemapped_left_edit_mod.jpg)
- **CLI**: bash polar -m rect2polar -r 0,m -v white rostock_laage_airport_cubemapped_left_edit_mod.jpg rostock_laage_airport_cubemapped_left_edit_mod_fix.jpg
![alt_text](5_redacted_edited_cubemap_pics//deeper/left/rostock_laage_airport_cubemapped_left_edit_mod_fix.jpg)

#### **Right**
![alt_text](5_redacted_edited_cubemap_pics//deeper/right/rostock_laage_airport_cubemapped_right.jpg)
- **GIMP**: paste one of the QR codes in rostock_laage_airport_cubemapped_right.jpg
![alt_text](5_redacted_edited_cubemap_pics//deeper/right/rostock_laage_airport_right_edit_redacted.jpg)
- **GIMP**: Photoshop the projector in the picture to be fully black and use a slightly lighter shade of black (closer to red) for the inner transparent pixels of the QR code
![alt_text](5_redacted_edited_cubemap_pics//deeper/right/rostock_laage_airport_sightings_right.jpg)

### **Step 6: Reassemble into Flattened Spherical Panorama**
- **Folder**: `6_assembled_modified_cubemap_pics`
- **Procedure**: Use the edited cubemap faces to reassemble them into a flattened spherical panorama format.
- **Description**: The modified cubemap is converted back into a spherical panorama format (**8192x4096**).
- **Tools**: Fred's ImageMagick Scripts: cube2sphericalpano script.
- **CLI**:  bash cube2sphericalpano -d 8192x4096 rostock_laage_airport_left_edit_redacted.jpg rostock_laage_airport_front_edit_redacted.jpg rostock_laage_airport_right_edit_redacted.jpg rostock_laage_airport_back_edit_redacted.jpg rostock_laage_airport_over_edit_redacted.jpg rostock_laage_airport_under_edit_redacted.jpg rostock_laage_airport_sightings.png
- **Output**: This is the PNG spherical panorama containing the embedded QR code pieces.
![alt text](6_assembled_modified_cubemap_pics/sources/Downloaded_cube2sphericalpano_Script.png) ![alt text](6_assembled_modified_cubemap_pics/sources/Source_of_Cubemap_to_SphericalPano_Converter_Script_1.png) ![alt text](6_assembled_modified_cubemap_pics/sources/Source_of_Cubemap_to_SphericalPano_Converter_Script_2.png)
![alt text](6_assembled_modified_cubemap_pics/cli_executions/cube2sphericalpano_command.png)

### **Step 7: Convert to Uploadable JPG**
- **Folder**: `7_final_spherical_panorama`
- **Procedure**: Convert the final flattened spherical panorama into a JPG format to reduce its size from 147MB to 8MB without losing necessary image quality.
- **Description**: The produced spherical panorama that will be shown to participants in an HTML file.
- **Tools**: ImageMagick's convert command.
- **CLI**:  convert rostock_laage_airport_sightings.png rostock_laage_airport_sightings.jpg
- **Output**: This is the final JPG spherical panorama containing the embedded QR code pieces.
![alt text](7_final_spherical_panorama/cli_executions/convert_png_to_jpg_command.png)

### **Step 8: Embed Base64 encoded image into HTML file which uses Pannellum**
- **Folder**: `8_html_file_creation`
- **Procedure**: Encode the image into Base64 and paste it into an HTML file relying on a simple open-source JS tool (Pannellum) for displaying panoramic images in a 360 degree environment.
- **Description**: This HTML file is the only thing the participants will have access to. By downloading and double-clicking on this simple HTML file, they will be able to easily view the panoramic image in a 360-degree environment. The HTML file is called "pano_display.html"
- **Tools**: Pannellum, and Base64Encoder (https://www.base64encoder.io/image-to-base64-converter/)
![alt text](8_html_file_creation/sources/Base64Encoder_example.png) ![alt text](8_html_file_creation/sources/html_file_contents_shown.png)

---

## Tools, Sites, & Techniques
### **Tools Used in the Design Phase**
1. **Fred's ImageMagick Scripts**:
   - Website belonging to Fred Weinhaus containing many image-related scripts including ones for converting between spherical panoramas and cubemap formats, and rect to polar conversion. (http://www.fmwconcepts.com/imagemagick/index.php)
2. **GIMP**:
   - For editing QR code pieces and embedding them into cubemap faces. (https://www.gimp.org/downloads/)
3. **ImageMagick Linux CLI library**:
   - Library used for image processing like splitting images and converting from png to jpg. (sudo apt install ImageMagick)
4. **Canva**:
   - For QR code generation. (https://www.canva.com/qr-code-generator/)
5. **PolyHaven**:
   - Free, community-driven platform providing high-quality, royalty-free digital assets such as HDRIs (High Dynamic Range Images), 3D models, and textures. (https://polyhaven.com/a/rostock_laage_airport)
6. **Pannellum**:
   - Lightweight, free, and open source panorama viewer for the web. Built using HTML5, CSS3, JavaScript, and WebGL, it is plug-in free. (https://pannellum.org/)
7. **Base64Encoder**:
   - Online tool used to encode images to Base64 (https://www.base64encoder.io/image-to-base64-converter/)

---

## Acknowledgments
This CTF challenge was inspired by the intersection of steganography, 360-degree imaging, and creative problem-solving. Special thanks to open-source tools like Linux, ImageMagick, GIMP, 
Pannellum, as well as Microsoft Paint, Base64Encoder, Canva, PolyHaven, and Fred Weinhaus's "free of charge for non-commercial (non-profit) use, ONLY" ImageMagick scripts for allowing the workflow to be seamless.

---

**Prepared by:** Serban Alin Caia
**Date:** 2025/03/09
