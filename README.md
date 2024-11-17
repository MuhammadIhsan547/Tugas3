# AplikasiDiskon
 Tugas3 - Muhammad Ihsan - 2210010286
# Aplikasi Perhitungan Diskon

**Tugas 3 - Muhammad Ihsan**  
**NPM 2210010286**  
**Kelas 5A TI Reg Pagi BJM**

---

## Deskripsi Program

Aplikasi ini memungkinkan pengguna untuk menghitung harga akhir setelah diskon berdasarkan harga asli yang dimasukkan. Pengguna dapat memilih diskon melalui pilihan persentase dari combo box atau slider. Selain itu, aplikasi ini juga mendukung penggunaan kode kupon untuk mendapatkan diskon tambahan.

---

## Komponen GUI

- **JFrame, JPanel, JLabel, JTextField, JComboBox, JButton, JSlider**
  - **JLabel** untuk judul aplikasi, seperti "Aplikasi Perhitungan Diskon".
  - **JLabel** untuk label "Harga Asli", **JTextField** untuk input harga asli (dengan nama `HargaAwal`).
  - **JLabel** untuk label "Persentase Diskon", **JComboBox** (dengan nama `ComboBoxDiskon`) untuk pilihan persentase diskon (0%, 10%, 20%, ..., 100%).
  - **JButton** dengan teks "Hitung" untuk menghitung diskon.
  - **JLabel** untuk label "Harga Akhir" dan **JTextField** untuk menampilkan hasil harga akhir (`HargaAkhir`).
  - **JLabel** untuk label "Penghematan" dan **JTextField** untuk menampilkan jumlah penghematan (`Keuntungan`).
  - **JSlider** untuk memilih persentase diskon dan menampilkan nilai diskon di **JLabel** (`LabelPersentase`).

---

## Logika Program

- **Perhitungan Aritmatika**: Menghitung penghematan dan harga akhir berdasarkan harga asli dan diskon yang diterapkan.
- **Penanganan Eksepsi**: Menangani kesalahan input, seperti memasukkan harga yang tidak valid.

---

## Events

### ActionListener untuk tombol "Hitung"
```java
private void HitungActionPerformed(java.awt.event.ActionEvent evt) {
    try {
        if (HargaAwal.getText().isEmpty() || HargaAwal.getText().equals("Rp ")) {
            JOptionPane.showMessageDialog(this, "Silakan masukkan harga asli.", "Error", JOptionPane.ERROR_MESSAGE);
            return;
        }

        // Ambil HargaAwal dan Diskon Persen
        double hargaAwal = Double.parseDouble(HargaAwal.getText().replace("Rp ", "").replace(",", ""));
        int DiskonPersen = (SliderDiskon.getValue() > 0) ? SliderDiskon.getValue() : Integer.parseInt(((String) ComboBoxDiskon.getSelectedItem()).replace("%", ""));

        // Validasi kode kupon
        String kodeKupon = KodeKupon.getText().trim();
        if (kodeKupon.equalsIgnoreCase("DISKON5%")) {
            DiskonPersen += 5;
            JOptionPane.showMessageDialog(this, "Kode kupon 5% berhasil diterapkan!", "Info", JOptionPane.INFORMATION_MESSAGE);
        }

        // Hitung Penghematan dan Harga Akhir
        double keuntungan = hargaAwal * DiskonPersen / 100;
        double hargaAkhir = hargaAwal - keuntungan;

        // Tampilkan hasil
        Keuntungan.setText("Rp " + String.format("%,.2f", keuntungan));
        HargaAkhir.setText("Rp " + String.format("%,.2f", hargaAkhir));

        // Tambahkan hasil ke riwayat
        String hasilRiwayat = "Harga Awal: Rp " + String.format("%,.2f", hargaAwal) + 
                              ", Diskon: " + DiskonPersen + "%" + 
                              ", Penghematan: Rp " + String.format("%,.2f", keuntungan) + 
                              ", Harga Akhir: Rp " + String.format("%,.2f", hargaAkhir) + "\n";
        Riwayat.append(hasilRiwayat);
    } catch (NumberFormatException e) {
        JOptionPane.showMessageDialog(this, "Masukkan nilai yang valid.", "Error", JOptionPane.ERROR_MESSAGE);
    }
}
```

### ItemListener pada JComboBox untuk memilih persentase diskon
```java
private void ComboBoxDiskonItemStateChanged(java.awt.event.ItemEvent evt) {
    if (evt.getStateChange() == java.awt.event.ItemEvent.SELECTED) {
        String diskonStr = (String) ComboBoxDiskon.getSelectedItem();
        int DiskonPersen = Integer.parseInt(diskonStr.replace("%", ""));
    }
}
```

### StateChanged pada JSlider
```java
private void SliderDiskonStateChanged(javax.swing.event.ChangeEvent evt) {
    int sliderValue = SliderDiskon.getValue();
    LabelPersentase.setText("Persentase Diskon : " + sliderValue + "%");
}
```

---

## Variasi
- **Kode Kupon**: Pengguna dapat memasukkan kode kupon untuk mendapatkan diskon tambahan, seperti `DISKON5%`, `DISKON10%`, dll.
- **Slider Diskon**: Sebagai alternatif dari JComboBox untuk memilih persentase diskon.
- **Riwayat Perhitungan**: Hasil perhitungan harga asli, diskon, penghematan, dan harga akhir ditambahkan ke dalam riwayat perhitungan.

---

## Contoh Gambar Project Setelah di Run

![Tugas3](https://github.com/user-attachments/assets/2d814c75-9da0-49ac-9bd6-95ac57c92a28)


## Indikator Penilaian:

| No  | Komponen         |  Persentase  |
| :-: | --------------   |   :-----:    |
|  1  | Komponen GUI     |    20        |
|  2  | Logika Program   |    20        |
|  3  | Kesesuaian UI    |    15        |
|  4  | Constructor      |    15        |
|  5  | Memenuhi Variasi |    30        |
|     | **TOTAL**        | **100**      |

---

## Pembuat

Nama  : Muhammad Ihsan  
NPM   : 2210010286  
Kelas : 5A TI Reg Pagi BJM
