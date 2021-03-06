## `undefined` і `null`

JavaScript мае два розныя значэнні для 'нічога' - гэта `null` і `undefined`, пры
гэтым апошняе больш карыснае.

### Значэнне `undefined`

`undefined` — гэта тып з роўна адным значэннем: `undefined`.

Мова таксама аб'яўляе глабальную пераменную, што мае значэнне `undefined`; Гэта
пераменная таксама называецца `undefined`. Тым не менш, гэта пераменная, а **не**
канстанта, ці ключавое слова. Гэта азначае, што яе *значэнне* можа быць
з лёгкасцю перазапісаным.

> **Заўвага для ES5:** у ECMAScript 5 `undefined` **больш** *нельга запісваць* у
> строгім рэжыме, але гэта імя можа ўся яшчэ быць перакрыта праз выкарыстанне
> функцыі з іменем `undefined`.

Ніжэй пералічаныя некалькі выпадкаў, калі вяртаецца `undefined`:

 - Доступ да (немадыфікаванай) глабальнай пераменнай `undefined`.
 - Доступ да аб'яўленай, *але яшчэ не* ініцыалізаванай пераменнай.
 - Няяўна вернутае значэнне функцыі праз адсутнасць аператара `return`.
 - З аператара `return`, які нічога яўна не вяртае.
 - У выніку пошуку неіснуючай уласцівасці аб'екта.
 - Параметры функцыі, якім яўна не было прысвоена значэнне.
 - Усё, чаму было прысвоена значэнне `undefined`.
 - Любы выраз у форме `void(expression)`.

### Апрацоўка зменаў значэння `undefined`

З той прычыны, што глабальная пераменная `undefined` утрымлівае толькі копію
актуальнага *значэння* `undefined`, прысвойванне ёй новага значэння **не** мяняе
значэнне *тыпа* `undefined`.

Таксама для таго, каб параўнаць што-небудзь з значэннем `undefined`, спачатку
трэба атрымаць значэнне `undefined`.

Звыклая тэхніка абароны ад магчымага перазапісвання пераменнай `undefined` —
дадатковы параметр у [ананімнай абгортцы](#function.scopes), што выкарыстоўвае
адсутны аргумент.

    var undefined = 123;
    (function(something, foo, undefined) {
        // цяпер undefined у лакальнай зоне бачнасці
        // зноў спасылаецца на значэнне `undefined`

    })('Hello World', 42);

Гэтага ж выніку можна дасягнуць праз аб'яўленне ўнутры абгорткі.

    var undefined = 123;
    (function(something, foo) {
        var undefined;
        ...

    })('Hello World', 42);

Адзіная розніца ў тым, што гэта апошняя версія будзе большай на 4 байты пры
мініфікацыі, а ў першым унутры ананімнай абгорткі не будзе аператара `var`.

### Выкарыстоўванне `null`

Хаця `undefined` у кантэксце мовы JavaScript у асноўным выкарыстоўваецца ў сэнсе
традыйнага *null*, сам `null` (і літэрал і тып) з'яўляецца яшчэ адным тыпам дадзеных.

Выкарыстоўваецца ў некаторых унутранных механізмах JavaScript (напрыклад аб'яўленне
канца ланцужка прататыпаў пазначаючы `Foo.prototype = null`), але амаль што ва ўсіх
выпадках ён можа быць заменены на `undefined`.
