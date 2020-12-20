## Kumpulan Perintah Artisan

**php artisan serve** *//server artisan*

**php artisan make:controller SiswaController** *//buat controller*

**php artisan make:model Siswa** *//buat model siswa*

**php artisan make:migration create_siswa_table** *//buat migration siswa*

**php artisan make:model Siswa -m** *//buat model sekaligus migration tablenya -m artinya migration*

### Cara bypass data tanpa pake controller

Berikut ini cara bypass data pake compact

```php
Route::get('siswa', function() {
    $siswa = ['Rasmus Lerdorf','Taylor Otwell','Brendan Eich','John Resig'];
    //agar siswa dibaca kosong maka buat seperti ini $siswa = [];
    return view('siswa.index',compact('siswa'));
});
```

Berikut ini cara bypass data pake with

```php
Route::get('siswa', function() {
    $halaman = 'siswa'; //ini penanda halaman di menu yang aktif
    $siswa = ['Rasmus Lerdorf','Taylor Otwell','Brendan Eich','John Resig'];
    return view('siswa.index')->with('siswa', $siswa)->with('halaman', $halaman);
});

```

Berikut ini cara bypass data pake tanda =>

```php
Route::get('siswa', function() {
     $siswa = ['Rasmus Lerdorf','Taylor Otwell','Brendan Eich','John Resig'];
     return view('siswa.index',['siswa' => $siswa]);
});

```

### Cara bypass data lewat controller

kode routenya seperti ini

Route::get('siswa','SiswaController@index');

Kode di controllernya seperti ini

```php
class SiswaController extends Controller
{
  public function index(){
        $halaman = 'siswa';
        $siswa_list = Siswa::all();
        $jumlah_siswa = $siswa_list->count(); //menampilkan jumlah siswa
        return view('siswa.index', compact('halaman','siswa_list','jumlah_siswa'));
  }
}
```

### Buat tabel pake migration

1. Pastikan sudah buat database dan setting file .env
2. Buka cmd di folder laravelnya dan ketik perintah artisan migration
3. 

### Cara isi database lewat route laravel

```php
Route::get('sampledata', function() {
    DB::table('siswa')->insert([
    	[
    		'nisn' => '1004',
    		'nama_siswa' => 'Fiki Erza Saputra',
    		'tanggal_lahir' => '1990-02-12',
    		'jenis_kelamin' => 'L',
    		'created_at' => '2020-03-10 19:00:15',
    		'updated_at' => '2020-03-10 19:00:15',
    	],
    	[
    		'nisn' => '1005',
    		'nama_siswa' => 'Putri Azzahra',
    		'tanggal_lahir' => '1990-02-12',
    		'jenis_kelamin' => 'P',
    		'created_at' => '2020-03-10 19:00:15',
    		'updated_at' => '2020-03-10 19:00:15',
    	],
    	[
    		'nisn' => '1006',
    		'nama_siswa' => 'Diki Erdanisa',
    		'tanggal_lahir' => '1991-02-12',
    		'jenis_kelamin' => 'L',
    		'created_at' => '2020-03-10 19:00:15',
    		'updated_at' => '2020-03-10 19:00:15',
    	],
   	]);
});
```

cara menjalankan **localhost:8000/sampledata**
