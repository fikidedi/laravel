## Welcome to GitHub Pages

You can use the [editor on GitHub](https://github.com/fikidedi/laravel/edit/main/README.md) to maintain and preview the content for your website in Markdown files.

Whenever you commit to this repository, GitHub Pages will run [Jekyll](https://jekyllrb.com/) to rebuild the pages in your site, from the content in your Markdown files.

### Cara bypass data tanpa pake controller

Berikut ini cara bypass data pake compact

```
Route::get('siswa', function() {
    $siswa = ['Rasmus Lerdorf','Taylor Otwell','Brendan Eich','John Resig'];
    //agar siswa dibaca kosong maka buat seperti ini $siswa = [];
    return view('siswa.index',compact('siswa'));
});
```

Berikut ini cara bypass data pake with

```
Route::get('siswa', function() {
	  $halaman = 'siswa'; //ini penanda halaman di menu yang aktif
    $siswa = ['Rasmus Lerdorf','Taylor Otwell','Brendan Eich','John Resig'];
    return view('siswa.index')->with('siswa', $siswa)->with('halaman', $halaman);
});

```

Berikut ini cara bypass data pake tanda =>

```
Route::get('siswa', function() {
     $siswa = ['Rasmus Lerdorf','Taylor Otwell','Brendan Eich','John Resig'];
     return view('siswa.index',['siswa' => $siswa]);
});

```

### Cara bypass data lewat controller

Buat route get nya dulu 

Route::get('siswa','SiswaController@index');

untuk buat file controller lewat artisan ketik peintah ini di cmd

php artisan make:controller SiswaController

```
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
