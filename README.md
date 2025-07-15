<!DOCTYPE html>
<html lang="fa" dir="rtl">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>بنر ساز حرفه‌ای</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <script src="https://html2canvas.hertzen.com/dist/html2canvas.min.js"></script>
  <style>
    @font-face {
      font-family: 'Vazir';
      src: url('https://cdn.fontcdn.ir/Font/Persian/Vazir/Vazir.ttf');
    }
    * {
      font-family: 'Vazir', sans-serif;
    }
    #bannerPreview {
      background-size: cover;
      background-position: center;
      transition: all 0.3s ease;
    }
    #aboutModal {
      display: none;
    }
    #aboutModal.show {
      display: flex;
    }
  </style>
</head>
<body class="bg-gradient-to-br from-blue-100 via-white to-green-100 min-h-screen flex items-center justify-center p-4">
  <div class="bg-white rounded-2xl shadow-2xl p-6 w-full max-w-2xl">
    <div class="flex justify-between items-center mb-6">
      <h1 class="text-3xl font-extrabold text-blue-600">بنر ساز حرفه‌ای</h1>
      <button id="aboutBtn" class="bg-gray-100 text-gray-700 px-4 py-2 rounded-lg shadow hover:bg-gray-200">درباره</button>
    </div>
    <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
      <div>
        <label class="text-sm font-semibold">متن بنر</label>
        <input id="bannerText" type="text" class="mt-1 w-full p-2 border rounded-lg" placeholder="متن خود را وارد کنید" value="بنر نمونه">
      </div>
      <div>
        <label class="text-sm font-semibold">رنگ پس‌زمینه</label>
        <input id="bgColor" type="color" class="mt-1 w-full h-10 border rounded-lg" value="#2563eb">
      </div>
      <div>
        <label class="text-sm font-semibold">تصویر پس‌زمینه</label>
        <input id="bgImage" type="file" accept="image/*" class="mt-1 w-full p-2 border rounded-lg">
      </div>
      <div>
        <label class="text-sm font-semibold">رنگ متن</label>
        <input id="textColor" type="color" class="mt-1 w-full h-10 border rounded-lg" value="#ffffff">
      </div>
      <div>
        <label class="text-sm font-semibold">اندازه فونت</label>
        <input id="fontSize" type="number" class="mt-1 w-full p-2 border rounded-lg" value="24" min="10" max="100">
      </div>
      <div>
        <label class="text-sm font-semibold">نوع فونت</label>
        <select id="fontFamily" class="mt-1 w-full p-2 border rounded-lg">
          <option value="Vazir">وزیر</option>
          <option value="Arial">Arial</option>
          <option value="Times New Roman">Times New Roman</option>
        </select>
      </div>
    </div>
    <button id="downloadBtn" class="mt-6 w-full bg-blue-600 text-white font-bold p-3 rounded-xl shadow-lg hover:bg-blue-700 transition">📥 دانلود بنر</button>

    <div id="bannerPreview" class="mt-6 w-full h-48 flex items-center justify-center text-center rounded-xl border border-dashed border-gray-300" style="background-color: #2563eb; color: #ffffff; font-family: Vazir; font-size: 24px;">
      بنر نمونه
    </div>
  </div>

  <!-- Modal -->
  <div id="aboutModal" class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50">
    <div class="bg-white rounded-xl p-6 max-w-sm w-full shadow-xl">
      <h2 class="text-xl font-bold mb-4">درباره برنامه</h2>
      <p class="text-gray-700 mb-2">ایمیل: mahdishamiahar@gmil.com</p>
      <p class="text-gray-700 mb-2">توسعه‌دهنده: مهدی شامی</p>
      <p class="text-gray-700 mb-4">شماره: 09142500486</p>
      <button id="closeModalBtn" class="w-full bg-blue-100 text-blue-800 p-2 rounded-lg hover:bg-blue-200">بستن</button>
    </div>
  </div>

  <script>
    const bannerText = document.getElementById('bannerText');
    const bgColor = document.getElementById('bgColor');
    const bgImage = document.getElementById('bgImage');
    const textColor = document.getElementById('textColor');
    const fontSize = document.getElementById('fontSize');
    const fontFamily = document.getElementById('fontFamily');
    const bannerPreview = document.getElementById('bannerPreview');
    const downloadBtn = document.getElementById('downloadBtn');
    const aboutBtn = document.getElementById('aboutBtn');
    const aboutModal = document.getElementById('aboutModal');
    const closeModalBtn = document.getElementById('closeModalBtn');

    function updateBanner() {
      bannerPreview.textContent = bannerText.value;
      bannerPreview.style.backgroundColor = bgColor.value;
      bannerPreview.style.color = textColor.value;
      bannerPreview.style.fontSize = fontSize.value + 'px';
      bannerPreview.style.fontFamily = fontFamily.value;
    }

    bannerText.addEventListener('input', updateBanner);
    bgColor.addEventListener('input', updateBanner);
    textColor.addEventListener('input', updateBanner);
    fontSize.addEventListener('input', updateBanner);
    fontFamily.addEventListener('input', updateBanner);

    bgImage.addEventListener('change', function () {
      const file = bgImage.files[0];
      if (file) {
        const reader = new FileReader();
        reader.onload = function (e) {
          bannerPreview.style.backgroundImage = `url('${e.target.result}')`;
        };
        reader.readAsDataURL(file);
      } else {
        bannerPreview.style.backgroundImage = '';
      }
    });

    downloadBtn.addEventListener('click', function () {
      html2canvas(bannerPreview).then(canvas => {
        const link = document.createElement('a');
        link.download = 'banner.png';
        link.href = canvas.toDataURL('image/png');
        link.click();
      });
    });

    aboutBtn.addEventListener('click', () => aboutModal.classList.add('show'));
    closeModalBtn.addEventListener('click', () => aboutModal.classList.remove('show'));
    window.addEventListener('DOMContentLoaded', updateBanner);
  </script>
</body>
</html>
