# Flask Background Remover - Setup Instructions

## Project Structure
```
flask-bg-remover/
├── app.py                 # Main Flask application
├── requirements.txt       # Python dependencies
├── templates/
│   └── index.html        # HTML template
├── uploads/              # Temporary upload folder (auto-created)
├── outputs/              # Processed images folder (auto-created)
└── README.md            # This file
```

## Installation & Setup

### 1. Create Virtual Environment (Recommended)
```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

### 2. Install Dependencies
```bash
pip install -r requirements.txt
```

### 3. Create requirements.txt
```txt
Flask==2.3.3
rembg==2.0.50
Pillow==10.0.1
onnxruntime==1.16.0
```

### 4. Run the Application
```bash
python app.py
```

The application will be available at `http://localhost:5000`

## Features

- **Modern Professional UI**: Clean, responsive design with gradient backgrounds and smooth animations
- **Drag & Drop**: Simply drag images onto the upload area or click to browse
- **Real-time Processing**: Uses rembg AI model to remove backgrounds locally
- **Multiple Format Support**: PNG, JPG, JPEG, WEBP, BMP
- **File Size Validation**: Maximum 16MB file size limit
- **Preview Comparison**: Side-by-side view of original and processed images
- **Instant Download**: Download processed images as high-quality PNG
- **No External APIs**: Everything runs locally on your server
- **Automatic Cleanup**: Old files are automatically cleaned up
- **Mobile Responsive**: Works perfectly on all device sizes

## Security Features

- File type validation
- File size limits
- Secure filename handling
- Local processing (no data sent to external services)
- Automatic file cleanup to prevent storage bloat

## Usage

1. Open your browser and go to `http://localhost:5000`
2. Drag and drop an image or click to browse and select one
3. Wait for the AI to process the image (usually 5-15 seconds)
4. View the comparison between original and background-removed image
5. Click "Download Image" to save the result
6. Use "Process Another Image" to start over

## Technical Details

- **Backend**: Flask (Python web framework)
- **AI Model**: rembg (state-of-the-art background removal)
- **Image Processing**: PIL (Python Imaging Library)
- **Frontend**: Pure HTML/CSS/JavaScript with modern design
- **Icons**: Font Awesome
- **Responsive Design**: CSS Grid and Flexbox

## Customization

### Changing Upload Limits
Edit the `MAX_CONTENT_LENGTH` in `app.py`:
```python
app.config['MAX_CONTENT_LENGTH'] = 32 * 1024 * 1024  # 32MB
```

### Adding New File Formats
Update the `ALLOWED_EXTENSIONS` set in `app.py`:
```python
ALLOWED_EXTENSIONS = {'png', 'jpg', 'jpeg', 'webp', 'bmp', 'tiff'}
```

### Modifying AI Model
rembg supports different models. You can specify a model:
```python
from rembg import remove, new_session

# Use a specific model
session = new_session('u2net')  # or 'silueta', 'u2netp', etc.
output_data = remove(input_data, session=session)
```

## Production Deployment

For production deployment, consider:

1. **Use a Production WSGI Server**:
   ```bash
   pip install gunicorn
   gunicorn -w 4 -b 0.0.0.0:5000 app:app
   ```

2. **Set up Nginx as Reverse Proxy**
3. **Configure SSL/HTTPS**
4. **Set up Proper Logging**
5. **Configure File Upload Limits in Nginx**
6. **Set up Database for User Management** (if needed)
7. **Implement Rate Limiting**

## Troubleshooting

### Common Issues

1. **ONNX Runtime Error**: 
   ```bash
   pip install onnxruntime
   ```

2. **Memory Issues with Large Images**:
   - Reduce max file size
   - Add image resizing before processing

3. **Slow Processing**:
   - Consider using GPU-enabled onnxruntime-gpu
   - Implement image compression

4. **Port Already in Use**:
   ```bash
   python app.py
   # Change port in app.py: app.run(port=3000)
   ```

## License

This project is open source and available under the MIT License.