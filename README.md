<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">

  <title>Website Login Siswa</title>

  <style>

    *{
      margin:0;
      padding:0;
      box-sizing:border-box;
      font-family:Arial;
    }

    body{
      background:linear-gradient(135deg,#141e30,#243b55);
      min-height:100vh;
      display:flex;
      justify-content:center;
      align-items:center;
      color:white;
      padding:20px;
    }

    .box{
      width:100%;
      max-width:400px;
      background:rgba(255,255,255,0.1);
      backdrop-filter:blur(10px);
      padding:25px;
      border-radius:20px;
      box-shadow:0 10px 30px rgba(0,0,0,0.3);
    }

    h1{
      text-align:center;
      margin-bottom:20px;
    }

    input{
      width:100%;
      padding:12px;
      margin-bottom:15px;
      border:none;
      border-radius:10px;
      outline:none;
    }

    button{
      width:100%;
      padding:12px;
      border:none;
      border-radius:10px;
      background:#00b4db;
      color:white;
      font-size:16px;
      cursor:pointer;
      margin-top:10px;
    }

    button:hover{
      background:#0083b0;
    }

    .hidden{
      display:none;
    }

    .card{
      background:rgba(255,255,255,0.08);
      padding:15px;
      border-radius:15px;
      margin-top:15px;
    }

    .adminBtn{
      background:red;
    }

  </style>
</head>
<body>

<!-- LOGIN SISWA -->
<div class="box" id="loginSiswa">

  <h1>Login Siswa</h1>

  <input type="text" id="nama" placeholder="Nama siswa">

  <input type="text" id="kelas" placeholder="Kelas">

  <button onclick="loginSiswa()">
    Masuk
  </button>

  <button class="adminBtn" onclick="bukaAdmin()">
    Login Admin
  </button>

</div>

<!-- LOGIN ADMIN -->
<div class="box hidden" id="loginAdmin">

  <h1>Admin Panel</h1>

  <input type="password" id="passwordAdmin" placeholder="Password admin">

  <button onclick="loginAdmin()">
    Masuk Admin
  </button>

  <button onclick="kembali()">
    Kembali
  </button>

</div>

<!-- DASHBOARD ADMIN -->
<div class="box hidden" id="dashboard">

  <h1>Data Login Siswa</h1>

  <div id="data"></div>

  <button onclick="logoutAdmin()">
    Logout Admin
  </button>

</div>

<script>

let passwordAdmin = "admin123";

let dataSiswa =
JSON.parse(localStorage.getItem("dataSiswa")) || [];

function simpanData(){

  localStorage.setItem(
    "dataSiswa",
    JSON.stringify(dataSiswa)
  );

}

function loginSiswa(){

  let nama =
  document.getElementById("nama").value;

  let kelas =
  document.getElementById("kelas").value;

  if(nama==="" || kelas===""){

    alert("Isi nama dan kelas!");

    return;

  }

  dataSiswa.push({

    nama:nama,
    kelas:kelas,
    waktu:new Date().toLocaleString()

  });

  simpanData();

  alert("Login berhasil!");

  document.getElementById("nama").value = "";
  document.getElementById("kelas").value = "";

}

function bukaAdmin(){

  document.getElementById("loginSiswa")
  .classList.add("hidden");

  document.getElementById("loginAdmin")
  .classList.remove("hidden");

}

function kembali(){

  document.getElementById("loginAdmin")
  .classList.add("hidden");

  document.getElementById("loginSiswa")
  .classList.remove("hidden");

}

function loginAdmin(){

  let password =
  document.getElementById("passwordAdmin").value;

  if(password !== passwordAdmin){

    alert("Password admin salah!");

    return;

  }

  document.getElementById("loginAdmin")
  .classList.add("hidden");

  document.getElementById("dashboard")
  .classList.remove("hidden");

  tampilkanData();

}

function tampilkanData(){

  let box = document.getElementById("data");

  box.innerHTML = "";

  dataSiswa.forEach((item,index)=>{

    box.innerHTML += `

      <div class="card">

        <h3>${item.nama}</h3>

        <p>Kelas: ${item.kelas}</p>

        <p>${item.waktu}</p>

        <button onclick="hapus(${index})">
          Hapus
        </button>

      </div>

    `;

  });

}

function hapus(index){

  dataSiswa.splice(index,1);

  simpanData();

  tampilkanData();

}

function logoutAdmin(){

  document.getElementById("dashboard")
  .classList.add("hidden");

  document.getElementById("loginSiswa")
  .classList.remove("hidden");

}

</script>

</body>
</html>
