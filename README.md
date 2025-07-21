<!-- sender.html --><!DOCTYPE html><html lang="en">
<head>
  <meta charset="UTF-8" />
  <title>Camera Sender</title>
</head>
<body>
  <h2>📷 ক্যামেরা লাইভ শেয়ার (Sender)</h2>
  <video id="localVideo" autoplay muted playsinline style="width: 100%; max-width: 500px;"></video>
  <script>
    const video = document.getElementById('localVideo');
    const bc = new BroadcastChannel('camera-stream');navigator.mediaDevices.getUserMedia({ video: true, audio: false })
  .then(stream => {
    video.srcObject = stream;

    const recorder = new MediaRecorder(stream);
    recorder.ondataavailable = e => bc.postMessage(e.data);
    recorder.start(100);
  })
  .catch(err => alert('Camera access denied or not available.'));

  </script>
</body>
</html>
