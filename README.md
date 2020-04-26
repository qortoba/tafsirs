# Quran Tafsirs
Quran tafsirs in HTML format. Available to use in any app/website.

## Tafsir File Format
Tafsir files are HTML files that contain chapters. Each chapter follow a very specific structure like this:

```
<div class="role-section1" data-chtitle="سورة البقرة (آية ١ – ٣٣)" id="ch2">
    <h1 id="69.lWdVO">سورة البقرة (آية ١ – ٣٣)</h1>
    <div class="surah_tafsir">
        <div class="verse-tafsir" data-verse="2:1">
        ...
        </div>
        <div class="verse-tafsir" data-verse="2:2">
        ...
        </div>
        ...
    </div>
</div>
```

* Each chapter is a tafsir of an entire surah or part of a surah. A chapter cannot contain tafsir from multiple surahs.
* The contents of each chapter are wrapped in `<div class="surah_tafsir">`
* The tafsir for each verse or set of verses is wrapped in `<div class="verse-tafsir" data-verse="2:1">`
* The attribute `data-verse` identifies the set of verses the tafsir applies to. This is used to find tafsir for a specific verse. For example `data-verse="2:5"` means it is the tafsir for surah 2 verse 5. Sometimes the tafsir applies to a range of verses in this case it looks like this: `data-verse="2:1-5"` which means this tafsir is for surah 2 verses 1 through 5 (including verses 1, 2, 3, 4 and 5).

### Verse Tafsir Format
Inside each `<div class="verse-tafsir">` there is a specific structure for the verse tafsir. It starts with the verse itself then followed by a `<div class="tafsir">` which contains the HTML-formatted tafsir text. Here's an example:
```
<div class="verse-tafsir" data-verse="2:1">
   <!-- this is the verse or verses that the tafsir applies to -->
    <span class="vo">
        <span class="vb">﴿</span>
        <span class="v" id="qr-alrazy-2-1">الم</span>
        <a class="vl" data-v="2:1" href="/quran/2/1" target="_blank" title="سورة البقرة">﴿١﴾</a>
        <span class="ve">﴾</span>
    </span>
    <!-- this is the actual tafsir -->
    <div class="tafsir">
        <p id="69.LAJZO">
            <span class="sh">تفسير آلم حروف الهجاء:</span>
            <span class="vo">
                <span class="vb">﴿</span>
                <span class="v">الم</span>
                <span class="ve">﴾</span>
            </span>فيه مسألتان: المسألة الأولى:</p>
        <p id="69.yKW9G">اعلم أن الألفاظ التي يتهجى بها أسماء مسمياتها الحروف المبسوطة، لأن الضاد مثلاً لفظة مفردة دالة بالتواطؤ على معنى مستقل بنفسه من غير دلالة على الزمان المعين لذلك المعنى، وذلك المعنى هو الحرف الأول من ضرب فثبت أنها أسماء ولأنها يتصرف فيها بالأمالة والتفخيم والتعريف والتنكير والجمع والتصغير والوصف والإسناد والإضافة، فكانت لا محالة أسماء.</p>
    </div>
</div>
```
Note that the verse itself is contained in `<span class="vo">` and it is wrapped in the verse brackets. This is the standard format for Quran verses across the all books.

## Permalink Ids
You may have noticed in the above examples that all `<p>` and `<h1>, <h2>, <h3>` elements have ids like `id="69.yKW9G"`. These are unique ids assigned during the tafsir publishing process. They can be used to link directly to a section (i.e. a heading) or a paragraph. The goal is to allow the user to copy a link to any section or paragraph so they can save that link in their own notes or share it in social media.

## Finding The Right Tafsir File
Say the user wants to read tafsir of Imam Al-Razi for surah 2 verse 10. The content is stored in `./content/alrazy/`. But which content file should we open to find the tafsir for verse 2:10? This tafsir is very long so the tafsir for surah 2 (Al Baqarah) is split across 8 files named `alrazy_002_01.xml, alrazy_002_02.xml, alrazy_002_03.xml, ..., alrazy_002_08.xml`. It would be very slow to open each file and look for tafsir for verse number 10. To solve this, we generate a file called surah_map.json which contains a map from verse number to file. For example:

```
"2": [
        {
            "end": "33",
            "file": "alrazy_002_01.xml",
            "start": "1"
        },
        {
            "end": "64",
            "file": "alrazy_002_02.xml",
            "start": "34"
        },
        {
            "end": "121",
            "file": "alrazy_002_03.xml",
            "start": "65"
        },
```

This is the entry for sura 2. It is saying that verses 1 to 33 are in file `alrazy_002_01.xml` and verses 34 to 64 are in `alrazy_002_02.xml` etc. This json map is generated when the tafsir is published and is stored in `surah_map.json` in the tafsir directory i.e. `./content/alrazy/`.

## Finding The Right verse-tafsir div
Once you know the file you want, you can open it with your favorite HTML/XHTML parser to look for the `<div class="verse-tafsir">` for the desired verse. You can do this by looping through all `<div class="verse-tafsir">` elements and checking their `data-verse="2:1"` attributes to find the one that contains the verse you are looking for. You can then show this entire `div` to the user. Note that some tafsirs don't have each verse tafsir broken out separately because some verses belong together and should be understood together.

## Typos and Errors
These tafsirs were manually typed and reviewed but it's not possible to catch all typos and errors. If you see an error please fix it and send a PR. Thank you!

# Tafsir Index
See [this readme](/content/README.md) for a list of available
