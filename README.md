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
    .navbar-brand { font-weight: bold; color: #0d6efd !important; }
    .card { border: none; border-radius: 12px; box-shadow: 0 4px 12px rgba(0,0,0,0.05); }
    .btn-primary { background-color: #0d6efd; border: none; border-radius: 8px; }
  </style>
</head>
<body>
  <nav class="navbar navbar-expand-lg navbar-light bg-white border-bottom shadow-sm">
    <div class="container">
      <a class="navbar-brand" href="#"><i class="bi bi-lightning-charge-fill me-1"></i> شعاع - فرع أبيس</a>
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
              <label class="form-label">رقم المشترك (13 رقم)</label>
              <input type="text" class="form-control" placeholder="أدخل رقم المشترك" required>
            </div>
            <div class="mb-3">
              <label class="form-label">قراءة العداد الحالية</label>
              <input type="number" class="form-control" placeholder="أدخل القراءة" required>
            </div>
            <div class="mb-3">
              <label class="form-label">صورة العداد</label>
              <input type="file" class="form-control" accept="image/*" required>
            </div>
            <button type="submit" class="btn btn-primary w-100 py-2">إرسال القراءة</button>
          </form>
        </div>
      </div>
    </div>
  </div>

  <div class="container py-4 d-none" id="adminView">
    <h4 class="mb-4">لوحة تحكم فرع أبيس</h4>
    <div class="card p-3">
      <div class="table-responsive">
        <table class="table table-hover align-middle">
          <thead>
            <tr>
              <th>رقم المشترك</th>
              <th>القراءة</th>
              <th>التاريخ</th>
              <th>الحالة</th>
            </tr>
          </thead>
          <tbody>
            <tr>
              <td>1020304050607</td>
              <td>14580 kWh</td>
              <td>اليوم 08:30 م</td>
              <td><span class="badge bg-warning text-dark">قيد المراجعة</span></td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>

  <script>
    document.getElementById('toggleView').addEventListener('click', function() {
      const client = document.getElementById('clientView');
      const admin = document.getElementById('adminView');
      if (client.classList.contains('d-none')) {
        client.classList.remove('d-none');
        admin.classList.add('d-none');
        this.textContent = 'لوحة التحكم';
      } else {
        client.classList.add('d-none');
        admin.classList.remove('d-none');
        this.textContent = 'شاشة المشترك';
      }
    });

    document.getElementById('readingForm').addEventListener('submit', function(e) {
      e.preventDefault();
      alert('تم إرسال القراءة بنجاح!');
      this.reset();
    });
  </script>
</body>
</html>
