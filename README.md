# amitbanshiwalphoto
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Photo Upload & Download App</title>
  <style>
    body {
      font-family: sans-serif;
      text-align: center;
      margin-top: 50px;
    }
    #preview {
      margin-top: 20px;
      max-width: 90%;
      display: none;
      border: 1px solid #ccc;
      box-shadow: 0 0 10px #aaa;
    }
    button {
      margin-top: 10px;
      padding: 10px 20px;
      font-size: 16px;
    }
  </style>
</head>
<body>
  <h1>📷 Photo Upload & Download Website</h1>
  <input type="file" id="photoInput" accept="image/*">
  <br>
  <button onclick="downloadPhoto()">⬇ Download Photo</button>
  <br><br>
  <img id="preview" width="400" />
  <script src="app.js"></script>
</body>
</html>
let uploadedImageDataUrl = "";

document.getElementById('photoInput').addEventListener('change', function (e) {
  const file = e.target.files[0];
  if (file) {
    const reader = new FileReader();
    reader.onload = function(evt) {
      uploadedImageDataUrl = evt.target.result;
      const imgElem = document.getElementById('preview');
      imgElem.src = uploadedImageDataUrl;
      imgElem.style.display = "block";
    }
    reader.readAsDataURL(file);
  }
});

function downloadPhoto() {
  if (uploadedImageDataUrl) {
    const a = document.createElement('a');
    a.href = uploadedImageDataUrl;
    a.download = "downloaded_photo.png";
    document.body.appendChild(a);
    a.click();
    document.body.removeChild(a);
  } else {
    alert("⚠️ Pehle photo upload karein!");
  }
}
