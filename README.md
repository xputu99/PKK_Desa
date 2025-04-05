<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>PKK - Pemberdayaan Kesejahteraan Keluarga</title>
  <style>
    body { font-family: Arial, sans-serif; margin: 0; padding: 0; }
    header { background-color: #4CAF50; color: white; padding: 20px; text-align: center; }
    nav { background-color: #388E3C; padding: 10px; text-align: center; }
    nav a { color: white; margin: 0 15px; text-decoration: none; }
    nav a:hover { text-decoration: underline; }
    section { padding: 20px; }
    footer { background-color: #2E7D32; color: white; text-align: center; padding: 10px; }
    .product-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 20px; }
    .product { border: 1px solid #ccc; border-radius: 8px; padding: 10px; text-align: center; }
    .product img { max-width: 100%; height: auto; border-radius: 4px; }
    .order-form { margin-top: 20px; padding: 10px; border: 1px solid #ccc; border-radius: 8px; }
    .order-form input, .order-form textarea { width: 100%; padding: 8px; margin-bottom: 10px; border-radius: 4px; border: 1px solid #aaa; }
    .order-form button { background-color: #4CAF50; color: white; padding: 10px; border: none; border-radius: 4px; cursor: pointer; }
    .admin-dashboard { background-color: #f1f1f1; padding: 20px; border-radius: 8px; margin-top: 20px; }
    .admin-dashboard h3 { color: #333; }
    .admin-order { background-color: white; border: 1px solid #ccc; padding: 10px; margin-bottom: 10px; border-radius: 6px; }
  </style>
  <script type="text/javascript" src="https://cdn.emailjs.com/dist/email.min.js"></script>
  <script>
    (function(){
      emailjs.init("RyRuZX0ND72rAU2c-");
    })();

    const pesananMasuk = [];

    function kirimPesanan(namaProduk) {
      const nama = document.getElementById('nama-' + namaProduk).value;
      const alamat = document.getElementById('alamat-' + namaProduk).value;
      const telp = document.getElementById('telp-' + namaProduk).value;
      const catatan = document.getElementById('catatan-' + namaProduk).value;

      const templateParams = {
        user_name: nama,
        user_address: alamat,
        user_phone: telp,
        product_name: namaProduk,
        notes: catatan
      };

      emailjs.send('service_0my1zoe', 'template_rq4t2ib', templateParams)
        .then(function(response) {
          alert('Email konfirmasi telah dikirim ke admin!');
        }, function(error) {
          alert('Gagal mengirim email: ' + JSON.stringify(error));
        });

      const nomorWa = '6281234567890';
      const pesan = `Halo, saya ingin memesan *${namaProduk}*\nNama: ${nama}\nAlamat: ${alamat}\nNo. HP: ${telp}\nCatatan: ${catatan}`;
      const linkWa = `https://wa.me/${nomorWa}?text=${encodeURIComponent(pesan)}`;
      window.open(linkWa, '_blank');

      pesananMasuk.push({ namaProduk, nama, alamat, telp, catatan });
      tampilkanPesanan();
    }

    function tampilkanPesanan() {
      const list = document.getElementById('daftar-pesanan');
      list.innerHTML = '';
      pesananMasuk.forEach((p, i) => {
        const div = document.createElement('div');
        div.className = 'admin-order';
        div.innerHTML = `<strong>${i + 1}. ${p.namaProduk}</strong><br>Nama: ${p.nama}<br>Alamat: ${p.alamat}<br>Telp: ${p.telp}<br>Catatan: ${p.catatan}`;
        list.appendChild(div);
      });
    }
  </script>
</head>
<body>
<!-- ... isi halaman tetap sama ... -->
</body>
</html>
