# web-personal
web
<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Kantin Sekolah Sehat & Murah</title>
    <!-- Memuat Tailwind CSS untuk styling cepat dan responsif -->
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700&display=swap" rel="stylesheet">
    <style>
        /* Menggunakan font Inter dan warna dasar */
        body { 
            font-family: 'Inter', sans-serif; 
            /* Perubahan: Menambahkan background gradient yang lembut */
            background: linear-gradient(135deg, #f0fdf4 0%, #d1fae5 100%);
            min-height: 100vh; /* Memastikan gradient mencakup seluruh layar */
        }
        /* Mengatur scrollbar yang lebih halus */
        ::-webkit-scrollbar { width: 8px; }
        ::-webkit-scrollbar-thumb { background: #34d399; border-radius: 10px; }
        ::-webkit-scrollbar-track { background: #f1f1f1; }

        /* Gaya Khusus untuk Card Menu */
        .menu-card {
            /* Menambahkan efek shadow yang lebih dalam dan transisi hover */
            transition: all 0.3s ease;
            box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1), 0 4px 6px -2px rgba(0, 0, 0, 0.05);
            /* Menambahkan sedikit rotasi saat hover untuk efek 3D */
            transform: scale(1);
        }
        .menu-card:hover {
            box-shadow: 0 20px 25px -5px rgba(0, 0, 0, 0.15), 0 10px 10px -5px rgba(0, 0, 0, 0.08);
            transform: translateY(-5px) scale(1.02);
        }
        
        /* Gaya Khusus untuk Tombol Pesan */
        .order-button {
            /* Gradient pada tombol, shadow yang menonjol, dan efek saat diklik */
            background-image: linear-gradient(to right, #10b981 0%, #059669 100%);
            transition: all 0.2s ease;
            box-shadow: 0 4px 6px -1px rgba(16, 185, 129, 0.5), 0 2px 4px -2px rgba(16, 185, 129, 0.5);
        }
        .order-button:hover {
            opacity: 0.9;
            box-shadow: 0 10px 15px -3px rgba(16, 185, 129, 0.6), 0 4px 6px -4px rgba(16, 185, 129, 0.6);
        }
        .order-button:active {
            transform: scale(0.98);
        }

    </style>
</head>
<body class="text-gray-800">

    <!-- HEADER / JUDUL UTAMA -->
    <header class="bg-white shadow-xl sticky top-0 z-10">
        <div class="container mx-auto p-4 flex justify-between items-center">
            <h1 class="text-2xl font-bold text-green-700">Kantin Digital SMK</h1>
            <!-- Tombol Keranjang (selalu terlihat) -->
            <button id="toggleCartBtn" class="p-2 rounded-full bg-green-600 text-white hover:bg-green-700 transition duration-150 relative shadow-lg">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 3h2l.4 2M7 13h10l4-8H5.4M7 13L5.4 5M7 13l-2.293 2.293c-.63.63-.184 1.707.707 1.707H17m0 0a2 2 0 100 4 2 2 0 000-4zm-8 2a2 2 0 11-4 0 2 2 0 014 0z" />
                </svg>
                <span id="cartCount" class="absolute top-0 right-0 inline-flex items-center justify-center px-2 py-1 text-xs font-bold leading-none text-red-100 transform translate-x-1/2 -translate-y-1/2 bg-red-600 rounded-full">0</span>
            </button>
        </div>
    </header>

    <main class="container mx-auto p-4 md:p-8 grid grid-cols-1 lg:grid-cols-3 gap-8">
        
        <!-- BAGIAN KIRI: BERANDA & DAFTAR MENU -->
        <div class="lg:col-span-2 space-y-8">
            
            <!-- Halaman Beranda / Deskripsi (dengan shadow yang lebih halus) -->
            <section class="bg-white p-6 rounded-xl shadow-lg border-b-4 border-green-600">
                <h2 class="text-3xl font-extrabold text-gray-900 mb-2">Kantin Sekolah Sehat & Murah</h2>
                <p class="text-gray-600">Selamat datang di Kantin Digital! Kami menyediakan berbagai pilihan makanan dan minuman yang lezat, higienis, dan ramah di kantong siswa. Pesan kebutuhanmu sekarang juga tanpa perlu antri!</p>
            </section>

            <!-- Daftar Menu Kantin -->
            <section>
                <h2 class="text-2xl font-bold text-gray-900 mb-4 border-b pb-2">Daftar Menu Tersedia</h2>
                <div id="menuList" class="grid grid-cols-1 sm:grid-cols-2 xl:grid-cols-3 gap-6">
                    <!-- Cards Menu akan di-inject oleh JavaScript di sini -->
                </div>
            </section>
        </div>

        <!-- BAGIAN KANAN: KERANJANG & FORMULIR (Sidebar) -->
        <!-- Perubahan: Mengubah shadow sidebar menjadi lebih menonjol -->
        <div id="cartSidebar" class="lg:col-span-1 bg-white p-6 rounded-xl shadow-2xl transition-all duration-300 fixed inset-y-0 right-0 w-full lg:w-96 transform translate-x-full lg:translate-x-0 lg:static z-20 overflow-y-auto">
            
            <div class="flex justify-between items-center mb-6 border-b pb-3">
                <h2 class="text-2xl font-bold text-green-700">Keranjang Pesanan</h2>
                <!-- Tombol Tutup untuk mobile -->
                <button id="closeCartBtn" class="lg:hidden text-gray-500 hover:text-gray-800">
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
                    </svg>
                </button>
            </div>

            <!-- Daftar Item di Keranjang -->
            <div id="cartItems" class="space-y-4 mb-6">
                <!-- Item Keranjang akan di-inject oleh JavaScript di sini -->
                <p id="emptyCartMessage" class="text-gray-500 text-center">Keranjang masih kosong.</p>
            </div>

            <!-- Total Harga -->
            <div class="flex justify-between items-center text-xl font-bold pt-4 border-t-2 border-green-600">
                <span>Total Belanja:</span>
                <span id="cartTotal" class="text-green-700">Rp 0</span>
            </div>

            <!-- Formulir Pemesanan Online -->
            <form id="orderForm" class="mt-8 space-y-4">
                <h3 class="text-xl font-bold mb-4 text-gray-800">Formulir Pengambilan & Pembayaran</h3>
                
                <!-- Simulasi QRIS -->
                <div id="qrisDisplay" class="hidden p-4 bg-yellow-50 rounded-xl border border-yellow-300">
                    <p class="text-sm font-semibold text-gray-700 mb-2">Total yang harus dibayar:</p>
                    <p class="text-2xl font-extrabold text-green-700 mb-3 text-center"><span id="qrisTotalDisplay">Rp 0</span></p>
                    <div class="flex justify-center">
                        <!-- Placeholder QRIS Image -->
                        <img src="https://placehold.co/200x200/2ecc71/ffffff?text=QRIS+SCAN+ME" alt="QRIS Code Placeholder" class="w-32 h-32 rounded-lg shadow-md border-4 border-white">
                    </div>
                    <p class="text-center mt-3 text-sm text-yellow-800">Gunakan aplikasi pembayaran Anda untuk memindai kode di atas.</p>
                </div>

                <div>
                    <label for="pembeliNama" class="block text-sm font-medium text-gray-700">Nama Pembeli</label>
                    <input type="text" id="pembeliNama" required class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-green-500 focus:ring-green-500 p-2 border">
                </div>
                
                <div>
                    <label for="pembeliKelas" class="block text-sm font-medium text-gray-700">Kelas</label>
                    <input type="text" id="pembeliKelas" required class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-green-500 focus:ring-green-500 p-2 border">
                </div>
                
                <div>
                    <label for="catatanPesanan" class="block text-sm font-medium text-gray-700">Catatan Tambahan (Opsional)</label>
                    <textarea id="catatanPesanan" rows="3" class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-green-500 focus:ring-green-500 p-2 border"></textarea>
                </div>
                
                <!-- Tombol Kirim Pesanan menggunakan gaya baru dan teks konfirmasi bayar -->
                <button type="submit" id="kirimPesananBtn" class="w-full py-3 px-4 border border-transparent rounded-lg shadow-lg text-lg font-medium text-white bg-green-600 hover:bg-green-700 focus:outline-none focus:ring-4 focus:ring-offset-2 focus:ring-green-400 transition duration-150 disabled:bg-gray-400 disabled:shadow-none">
                    Kirim Pesanan & Konfirmasi Bayar (<span id="finalTotal">Rp 0</span>)
                </button>
            </form>

        </div>
    </main>
    
    <!-- MODAL (Popup) untuk pesan sukses/error -->
    <div id="messageModal" class="hidden fixed inset-0 bg-gray-600 bg-opacity-75 flex items-center justify-center z-50 transition-opacity duration-300">
        <div class="bg-white p-6 rounded-xl shadow-2xl max-w-sm w-full transform transition-all duration-300 scale-95">
            <h3 id="modalTitle" class="text-xl font-bold mb-3 text-green-600"></h3>
            <p id="modalMessage" class="text-gray-700 mb-4"></p>
            <button id="closeModalBtn" class="w-full py-2 bg-green-500 text-white rounded-lg hover:bg-green-600">Tutup</button>
        </div>
    </div>

    <script>
        // DATA MENU KANTIN
        const menuData = [
            // Gambar Nasi Goreng
            { 
                id: 1, 
                nama: "Nasi Goreng Ayam", 
                harga: 15000, 
                gambar: "https://placehold.co/400x300/f39c12/ffffff?text=Nasi+Goreng+Enak" 
            },
            // PERUBAHAN DI SINI: Mengganti placeholder Mie Ayam dengan URL gambar Mie Ayam
            { 
                id: 2, 
                nama: "Mie Ayam Bakso", 
                harga: 12000, 
                // URL gambar Mie Ayam yang lebih realistis dan menggoda
                gambar: "https://placehold.co/400x300/e67e22/ffffff?text=Mie+Ayam+Menggoda" 
            },
            { 
                id: 3, 
                nama: "Es Teh Manis", 
                harga: 4000, 
                gambar: "https://placehold.co/400x300/2ecc71/ffffff?text=Es+Teh" 
            },
            { 
                id: 4, 
                nama: "Gorengan (3pcs)", 
                harga: 3000, 
                gambar: "https://placehold.co/400x300/f1c40f/333333?text=Gorengan" 
            },
            { 
                id: 5, 
                nama: "Jus Alpukat", 
                harga: 8000, 
                gambar: "https://placehold.co/400x300/9b59b6/ffffff?text=Jus+Alpukat" 
            },
            { 
                id: 6, 
                nama: "Roti Bakar Keju", 
                harga: 7000, 
                gambar: "https://placehold.co/400x300/ff69b4/ffffff?text=Roti+Bakar"
            }
        ];

        // VARIABEL GLOBAL DAN ELEMEN DOM
        let cart = []; // Array untuk menyimpan item yang dipesan
        const menuListDiv = document.getElementById('menuList');
        const cartItemsDiv = document.getElementById('cartItems');
        const cartTotalSpan = document.getElementById('cartTotal');
        const finalTotalSpan = document.getElementById('finalTotal');
        const cartCountSpan = document.getElementById('cartCount');
        const orderForm = document.getElementById('orderForm');
        const kirimPesananBtn = document.getElementById('kirimPesananBtn');
        const emptyCartMessage = document.getElementById('emptyCartMessage');
        const cartSidebar = document.getElementById('cartSidebar');
        const toggleCartBtn = document.getElementById('toggleCartBtn');
        const closeCartBtn = document.getElementById('closeCartBtn');
        
        // Elemen untuk QRIS
        const qrisDisplayDiv = document.getElementById('qrisDisplay');
        const qrisTotalDisplay = document.getElementById('qrisTotalDisplay');
        
        // MODAL ELEMENTS
        const messageModal = document.getElementById('messageModal');
        const modalTitle = document.getElementById('modalTitle');
        const modalMessage = document.getElementById('modalMessage');
        const closeModalBtn = document.getElementById('closeModalBtn');

        // FUNGSI UTAMA

        // 1. Format Rupiah
        function formatRupiah(angka) {
            const numberString = angka.toString().replace(/[^,\d]/g, '');
            const split = numberString.split(',');
            const sisa = split[0].length % 3;
            let rupiah = split[0].substr(0, sisa);
            const ribuan = split[0].substr(sisa).match(/\d{3}/gi);

            if (ribuan) {
                const separator = sisa ? '.' : '';
                rupiah += separator + ribuan.join('.');
            }

            rupiah = split[1] !== undefined ? rupiah + ',' + split[1] : rupiah;
            return 'Rp ' + rupiah;
        }

        // 2. Render Daftar Menu
        function renderMenu() {
            menuListDiv.innerHTML = ''; // Kosongkan konten lama
            menuData.forEach(menu => {
                const menuCard = document.createElement('div');
                // Menggunakan class 'menu-card' untuk styling khusus
                menuCard.className = 'bg-white rounded-xl overflow-hidden menu-card'; 
                menuCard.innerHTML = `
                    <!-- Gambar Menu: Sumber gambar diambil dari properti 'gambar' dalam menuData -->
                    <img src="${menu.gambar}" onerror="this.onerror=null;this.src='https://placehold.co/400x300/cccccc/333333?text=Gambar+Tidak+Tersedia';" alt="${menu.nama}" class="w-full h-40 object-cover">
                    <div class="p-4 space-y-3">
                        <!-- Nama & Harga -->
                        <div class="flex justify-between items-start">
                            <h3 class="text-lg font-semibold text-gray-900">${menu.nama}</h3>
                            <span class="text-xl font-bold text-green-600">${formatRupiah(menu.harga)}</span>
                        </div>
                        <!-- Tombol Pesan: Menggunakan class 'order-button' untuk styling khusus -->
                        <button onclick="addToCart(${menu.id})" class="w-full py-2 text-white font-bold rounded-lg shadow-md order-button">
                            Pesan
                        </button>
                    </div>
                `;
                menuListDiv.appendChild(menuCard);
            });
        }

        // 3. Menghitung Total Keranjang
        function calculateTotal() {
            return cart.reduce((sum, item) => sum + (item.harga * item.qty), 0);
        }

        // 4. Update Tampilan Keranjang
        function updateCart() {
            cartItemsDiv.innerHTML = ''; // Kosongkan tampilan keranjang
            const total = calculateTotal();
            const itemCount = cart.reduce((sum, item) => sum + item.qty, 0);

            cartTotalSpan.textContent = formatRupiah(total);
            finalTotalSpan.textContent = formatRupiah(total);
            cartCountSpan.textContent = itemCount;

            // Update total QRIS dan tampilkan/sembunyikan
            qrisTotalDisplay.textContent = formatRupiah(total);
            qrisDisplayDiv.classList.toggle('hidden', cart.length === 0);
            
            // Kontrol pesan kosong
            emptyCartMessage.classList.toggle('hidden', cart.length > 0);

            // Kontrol tombol kirim pesanan
            kirimPesananBtn.disabled = cart.length === 0;

            cart.forEach(item => {
                const cartItemDiv = document.createElement('div');
                cartItemDiv.className = 'flex items-center justify-between p-3 bg-gray-100 rounded-lg shadow-sm';
                cartItemDiv.innerHTML = `
                    <div class="flex-1 min-w-0">
                        <p class="font-medium truncate">${item.nama} <span class="text-sm text-gray-500">(${formatRupiah(item.harga)})</span></p>
                        <p class="text-xs text-green-700 font-bold">${formatRupiah(item.harga * item.qty)}</p>
                    </div>
                    <div class="flex items-center space-x-2 ml-4">
                        <button onclick="updateQuantity(${item.id}, -1)" class="w-7 h-7 bg-red-500 text-white rounded-full hover:bg-red-600 text-lg leading-none transition duration-150 shadow-sm">-</button>
                        <span class="font-bold w-4 text-center">${item.qty}</span>
                        <button onclick="updateQuantity(${item.id}, 1)" class="w-7 h-7 bg-green-500 text-white rounded-full hover:bg-green-600 text-lg leading-none transition duration-150 shadow-sm">+</button>
                    </div>
                `;
                cartItemsDiv.appendChild(cartItemDiv);
            });
        }

        // 5. Tambah Item ke Keranjang
        function addToCart(id) {
            const menu = menuData.find(m => m.id === id);
            const existingItem = cart.find(item => item.id === id);

            if (existingItem) {
                existingItem.qty += 1;
            } else {
                cart.push({ ...menu, qty: 1 });
            }
            showModal('Berhasil!', `${menu.nama} ditambahkan ke keranjang.`);
            updateCart();
        }

        // 6. Mengubah Kuantitas (Jumlah Pesanan)
        function updateQuantity(id, change) {
            const itemIndex = cart.findIndex(item => item.id === id);
            
            if (itemIndex > -1) {
                cart[itemIndex].qty += change;
                
                // Hapus item jika kuantitas kurang dari 1
                if (cart[itemIndex].qty < 1) {
                    cart.splice(itemIndex, 1);
                }
            }
            updateCart();
        }

        // 7. Menampilkan Modal Pesan
        function showModal(title, message) {
            modalTitle.textContent = title;
            // Mengubah warna title modal sesuai keberhasilan
            modalTitle.classList.remove('text-red-600');
            modalTitle.classList.add(title === 'Berhasil!' ? 'text-green-600' : 'text-red-600');

            modalMessage.textContent = message;
            messageModal.classList.remove('hidden');
            // Menambahkan kelas untuk animasi masuk
            messageModal.querySelector('div').classList.remove('scale-95');
            messageModal.querySelector('div').classList.add('scale-100');
        }

        // 8. Menyembunyikan Modal Pesan
        function hideModal() {
            // Menambahkan kelas untuk animasi keluar
            messageModal.querySelector('div').classList.remove('scale-100');
            messageModal.querySelector('div').classList.add('scale-95');
            setTimeout(() => {
                messageModal.classList.add('hidden');
            }, 300); // Tunggu hingga animasi selesai
        }

        // 9. Event Listener untuk Form Pemesanan
        orderForm.addEventListener('submit', function(e) {
            e.preventDefault(); // Mencegah form melakukan reload halaman

            if (cart.length === 0) {
                showModal('Gagal!', 'Keranjang Anda kosong. Silakan pilih menu.');
                return;
            }

            const nama = document.getElementById('pembeliNama').value;
            const kelas = document.getElementById('pembeliKelas').value;
            const catatan = document.getElementById('catatanPesanan').value;
            const total = calculateTotal();

            // Format Pesanan (untuk simulasi pengiriman ke kasir)
            const orderDetails = {
                nama,
                kelas,
                catatan: catatan || 'Tidak ada catatan.',
                pembayaran: "QRIS (DIKONFIRMASI)", // Menambahkan detail pembayaran
                total: formatRupiah(total),
                items: cart.map(item => ({
                    nama: item.nama,
                    qty: item.qty,
                    subtotal: formatRupiah(item.harga * item.qty)
                }))
            };

            // SIMULASI PROSES PESANAN
            console.log("--- DETAIL PESANAN BARU ---");
            console.log(JSON.stringify(orderDetails, null, 2));

            // Tampilkan pesan sukses ke pengguna
            showModal('Pesanan Berhasil!', `Pesanan QRIS senilai ${formatRupiah(total)} telah dikonfirmasi. Silakan tunggu panggilan pengambilan pesanan atas nama ${nama} (Kelas ${kelas}).`);

            // Reset Keranjang dan Form
            cart = [];
            orderForm.reset();
            updateCart();
            
            // Tutup sidebar di tampilan mobile setelah kirim
            cartSidebar.classList.add('translate-x-full'); 
            document.body.classList.remove('overflow-hidden');
        });

        // Event listener untuk tombol buka/tutup keranjang (responsive)
        toggleCartBtn.addEventListener('click', () => {
            // Menambahkan overlay di mobile saat sidebar terbuka
            document.body.classList.add('overflow-hidden');
            cartSidebar.classList.remove('translate-x-full');
        });

        closeCartBtn.addEventListener('click', () => {
            // Menghapus overlay
            document.body.classList.remove('overflow-hidden');
            cartSidebar.classList.add('translate-x-full');
        });

        // Event listener untuk tombol tutup modal
        closeModalBtn.addEventListener('click', hideModal);

        // INISIALISASI
        window.onload = function() {
            renderMenu();
            updateCart();
        };

    </script>
</body>
</html>
