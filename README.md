#  Konsep Pemrograman Berorientasi Objek - Login dengan Persistence
---
## Tutorial Membuat Tabel pada Database : 
### 1. Membuat tabel dengan query sebagai berikut.

![image](https://github.com/user-attachments/assets/7064f9dc-3fae-42e7-9304-f30924370deb)

### 2.	Mengisi data pada tabel.

![image](https://github.com/user-attachments/assets/171320c0-6e11-49c4-8f6d-c28dfc15716a)

## Tutorial Membuat Persistence : 
### 1.	Pilih “New – Entity Classes From Database”.

![image](https://github.com/user-attachments/assets/585dc406-3b7a-4330-aa38-1cd95bd55032)

### 2.	Pilih koneksi database.

![image](https://github.com/user-attachments/assets/90f972e9-f351-46dc-ad18-e4b261c327f8)

### 3.	Pindahkan tabel yang dibutuhkan pada kotak sebelah kanan.

![image](https://github.com/user-attachments/assets/81b945cc-bb7d-4917-9c71-2700bb81ccce)

### 4. Pilih Next.

![image](https://github.com/user-attachments/assets/ef4d5a05-9d3e-4cb0-950a-a0bf75e3f9c1)

### 5. Pilih Finish.

![image](https://github.com/user-attachments/assets/7d01c49b-cd95-4d1e-937d-7d74499c40d2)

### 6.	Setelah membuat persistence, maka akan muncul package META-INF dan file Akun.java

![image](https://github.com/user-attachments/assets/f3924274-5b32-492f-b8a9-59f5b409cf69)

## Tutorial GUI dan Source Code : 
### 1.	Membuat Frame Gui “Login” dengan desain sebagai berikut.

![image](https://github.com/user-attachments/assets/ebf60d56-dedc-43e2-8d97-7f447d1fbfe9)

### 2.	Source Code dari frame “Login”.
<pre>
  private void btnLoginActionPerformed(java.awt.event.ActionEvent evt) {                                         
        // TODO add your handling code here:
        if (tfUser.getText().equals("") | tfPw.getText().equals("")) {
            JOptionPane.showMessageDialog(null, "Isi Terlebih Dahulu");
        } else {
            EntityManagerFactory emf = Persistence.createEntityManagerFactory("PertemuanDuaBelasPU");
            EntityManager em = emf.createEntityManager();

            em.getTransaction().begin();

            String user = tfUser.getText();
            String pw = tfPw.getText();
            Akun y = em.find(Akun.class, user);

            if (y == null) {
                JOptionPane.showMessageDialog(null, "Username tidak ditemukan");
            } else if (y.getPassword().equals(pw)) {
                JOptionPane.showMessageDialog(null, "WELCOME !!!!!!");
                Mata_kuliah p = new Mata_kuliah();
                p.setVisible(true);
                this.dispose();
            } else {
                JOptionPane.showMessageDialog(null, "Username atau Password salah!");
            }
            em.getTransaction().commit();
            em.close();
            emf.close();
        }
    }                                        

    private void jLabel4MouseClicked(java.awt.event.MouseEvent evt) {                                     
        // TODO add your handling code here:
        CreateAkun y = new CreateAkun();
        y.setVisible(true);
        this.dispose();
    }                                    

</pre>
### 3.	Membuat Frame Gui “Create Akun” dengan desain berikut.

![image](https://github.com/user-attachments/assets/3b57e6d5-4c49-43bc-aad8-460a1a83982e)

### 4.	Source code pada frame “Create Akun”.
<pre>
  private void btnCreateActionPerformed(java.awt.event.ActionEvent evt) {                                          
  if (tfUser.getText().equals("") || tfPw.getText().equals("")) {
            JOptionPane.showMessageDialog(null, "Isi semua data terlebih dahulu!");
        } else {
            String user, pw;
            user = tfUser.getText();
            pw = tfPw.getText();

            EntityManagerFactory emf = Persistence.createEntityManagerFactory("PertemuanDuaBelasPU");
            EntityManager em = emf.createEntityManager();
            em.getTransaction().begin();

            Matakuliah y = em.find(Matakuliah.class, user);
            if (y != null) {
                JOptionPane.showMessageDialog(null, "Username sudah ada, coba gunakan username lain");
                bersih();
            } else {
                Akun x = new Akun();
                x.setUsername(user);
                x.setPassword(pw);
                em.persist(x);

                em.getTransaction().commit();
                JOptionPane.showMessageDialog(null, "Akun sukses dibuat");

                bersih();
                Login z = new Login();
                z.setVisible(true);
                this.dispose();
            }
            em.close();
            emf.close();
        }
        
    }                                         

    private void jLabel4MouseClicked(java.awt.event.MouseEvent evt) {                                     
        // TODO add your handling code here:
        Login y = new Login();
        y.setVisible(true);
        this.dispose();
    }                                    

    public void bersih() {
        tfUser.setText("");
        tfPw.setText("");
    }
    
</pre>

## Simulasi
### 1.	Ketika belum memiliki akun, maka kita pilih “Create An Account” dan kita akan diarahkan pada halaman untuk membuat akun.

![image](https://github.com/user-attachments/assets/85c4e0df-8d9f-498b-a8fe-a3763d721188)

### 2.	Pada halaman buat akun, isi username dan password sesuai keinginan. Lalu pilih “Create” dan akan muncul pemberitahuan bahwa akun telah berhasil dibuat. Lalu pilih Ok.

![image](https://github.com/user-attachments/assets/e16445e1-15d5-4b20-9091-a881e841bdbe)

### 3.	Maka akan diarahkan Kembali pada halaman Login. Isi username dan password yang sudah dibuat. Lalu muncul pemberitahuan bahwa login berhasil. 

![image](https://github.com/user-attachments/assets/9332c0db-6155-4234-a11c-3342c8243bf1)

### 4.	Ketika proses login sudah berhasil, maka akan diarahkan pada menu utama yaitu data Mata kuliah. Ketika memilih logout maka akan kembali pada halaman awal login.

![image](https://github.com/user-attachments/assets/1f6626d7-135d-4d91-8aec-52cf05462602)
