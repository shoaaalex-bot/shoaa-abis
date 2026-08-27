<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>منصة شعاع - فرع أبيس</title>
  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.rtl.min.css" rel="stylesheet">
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap-icons@1.11.0/font/bootstrap-icons.css">
  <style>
    body { background-color: #f4f6f9; font-family: system-ui, -apple-system, sans-serif; }
    .card { border: none; border-radius: 12px; box-shadow: 0 4px 12px rgba(0,0,0,0.05); }
    .meter-img { width: 60px; height: 60px; object-fit: cover; border-radius: 6px; cursor: pointer; }
  </style>
</head>
<body>
  <nav class="navbar navbar-expand-lg navbar-light bg-white border-bottom shadow-sm">
    <div class="container">
      <a class="navbar-brand text-primary fw-bold" href="#"><i class="bi bi-lightning-charge-fill me-1"></i> شعاع - فرع أبيس</a>
      <button class="btn btn-sm btn-outline-primary" id="toggleView">لوحة التحكم</button>
    </div>
  </nav>

  <div class="container py-4" id="clientView">
    <div class="row justify-content-center">
      <div class="col-md-6">
        <div class="card p-4">
          <h4 class="text-center mb-4 text-primary">تسجيل قراءة العداد</h4>
          <form id="readingForm">
            <div class="mb-3">
              <label class="form-label">رقم المشترك</label>
              <input type="text" id="accNo" class="form-control" placeholder="أدخل رقم المشترك" required>
            </div>
            <div class="mb-3">
              <label class="form-label">قراءة العداد الحالية</label>
              <input type="number" id="meterVal" class="form-control" placeholder="أدخل القراءة" required>
            </div>
            <div class="mb-3">
              <label class="form-label">صورة العداد</label>
              <input type="file" id="meterImgInput" class="form-control" accept="image/*" required>
            </div>
            <button type="submit" class="btn btn-primary w-100 py-2">إرسال القراءة</button>
          </form>
        </div>
      </div>
    </div>
  </div>

  <div class="container py-4 d-none" id="adminView">
    <h4 class="mb-4">لوحة تحكم فرع أبيس (مراجعة القراءات)</h4>
    <div class="card p-3">
      <div class="table-responsive">
        <table class="table table-hover align-middle" id="readingsTable">
          <thead>
            <tr>
              <th>صورة العداد</th>
              <th>رقم المشترك</th>
              <th>القراءة</th>
              <th>الحالة</th>
            </tr>
          </thead>
          <tbody>
            <!-- تظهر القراءات والصور المرسلة هنا -->
          </tbody>
        </table>
      </div>
    </div>
  </div>

  <script>
    const toggleBtn = document.getElementById('toggleView');
    const clientView = document.getElementById('clientView');
    const adminView = document.getElementById('adminView');
    const form = document.getElementById('readingForm');
    const tableBody = document.querySelector('#readingsTable tbody');

    toggleBtn.addEventListener('click', () => {
      clientView.classList.toggle('d-none');
      adminView.classList.toggle('d-none');
      toggleBtn.textContent = clientView.classList.contains('d-none') ? 'شاشة المشترك' : 'لوحة التحكم';
    });

    form.addEventListener('submit', (e) => {
      e.preventDefault();
      const acc = document.getElementById('accNo').value;
      const val = document.getElementById('meterVal').value;
      const file = document.getElementById('meterImgInput').files[0];

      if (file) {
        const reader = new FileReader();
        reader.onload = function(evt) {
          const row = `
            <tr>
              <td><img src="${evt.target.result}" class="meter-img" onclick="window.open('${evt.target.result}')" title="اضغط للتكبير"></td>
              <td>${acc}</td>
              <td>${val} kWh</td>
              <td><span class="badge bg-warning text-dark">قيد المراجعة</span></td>
            </tr>
          `;
          tableBody.insertAdjacentHTML('afterbegin', row);
          alert('تم إرسال القراءة والصورة بنجاح!');
          form.reset();
        };
        reader.readAsDataURL(file);
      }
    });
  </script>
</body>
</html>
