# カレンダー

カレンダーは暦の最も代表的なインターフェースであるため、サポートするメソッドが用意されています


## カレンダーデータの取得

`{Array} koyomi.getCalendarData({String|Number} range);`

カレンダーデータを簡単に作成することのできるメソッドが用意されています  
一般的なカレンダーをテーブルタグで動的作成する際に、通常次のような処理が必要です  

  1. 曜日の始まりを決め、1日より前に幾つの空マスを用意しなければならないか計算
  2. 週の終わりを計算し、次の行にするための判定を行う
  3. 末日から週の終わりまで幾つの空マスで埋めるかを計算
  4. 複数月を処理する場合は、データを何度も取得し、上記を行う

しかし、先のメソッドを使用すると、これらを複雑な処理をViewコードで行う必要はありません

### データ

次のようなデータを取得することができます

```
koyomi.startMonth = 1;
koyomi.startWeek = '日';
var data = koyomi.getCalendarData('2015/4-2015/6');

// data ->
// [
//   { som: true , eom: false, year: 2015, month: 3, day: 29, week: 0, open: false, close: '定休日'    , holiday: ''          , sow: true , eow: false, events: [], ghost: true , block: '2015/04', weekNumber:  1 },
//   { som: false, eom: false, year: 2015, month: 3, day: 30, week: 1, open: true , close: ''          , holiday: ''          , sow: false, eow: false, events: [], ghost: true , block: '2015/04', weekNumber:  1 },
//   { som: false, eom: false, year: 2015, month: 3, day: 31, week: 2, open: true , close: ''          , holiday: ''          , sow: false, eow: false, events: [], ghost: true , block: '2015/04', weekNumber:  1 },
//     // (中略)
//   { som: false, eom: false, year: 2015, month: 4, day: 28, week: 2, open: true , close: ''          , holiday: ''          , sow: false, eow: false, events: [], ghost: false, block: '2015/04', weekNumber:  5 },
//   { som: false, eom: false, year: 2015, month: 4, day: 29, week: 3, open: false, close: '昭和の日'  , holiday: '昭和の日'  , sow: false, eow: false, events: [], ghost: false, block: '2015/04', weekNumber:  5 },
//   { som: false, eom: false, year: 2015, month: 4, day: 30, week: 4, open: true , close: ''          , holiday: ''          , sow: false, eow: false, events: [], ghost: false, block: '2015/04', weekNumber:  5 },
//   { som: false, eom: false, year: 2015, month: 5, day:  1, week: 5, open: true , close: ''          , holiday: ''          , sow: false, eow: false, events: [], ghost: true , block: '2015/04', weekNumber:  5 },
//   { som: false, eom: false, year: 2015, month: 5, day:  2, week: 6, open: false, close: '定休日'    , holiday: ''          , sow: false, eow: true , events: [], ghost: true , block: '2015/04', weekNumber:  5 },
//   { som: false, eom: false, year: 2015, month: 5, day:  3, week: 0, open: false, close: '定休日'    , holiday: '憲法記念日', sow: true , eow: false, events: [], ghost: true , block: '2015/04', weekNumber:  6 },
//   { som: false, eom: false, year: 2015, month: 5, day:  4, week: 1, open: false, close: 'みどりの日', holiday: 'みどりの日', sow: false, eow: false, events: [], ghost: true , block: '2015/04', weekNumber:  6 },
//   { som: false, eom: false, year: 2015, month: 5, day:  5, week: 2, open: false, close: 'こどもの日', holiday: 'こどもの日', sow: false, eow: false, events: [], ghost: true , block: '2015/04', weekNumber:  6 },
//   { som: false, eom: false, year: 2015, month: 5, day:  6, week: 3, open: false, close: '振替休日'  , holiday: '振替休日'  , sow: false, eow: false, events: [], ghost: true , block: '2015/04', weekNumber:  6 },
//   { som: false, eom: false, year: 2015, month: 5, day:  7, week: 4, open: true , close: ''          , holiday: ''          , sow: false, eow: false, events: [], ghost: true , block: '2015/04', weekNumber:  6 },
//   { som: false, eom: false, year: 2015, month: 5, day:  8, week: 5, open: true , close: ''          , holiday: ''          , sow: false, eow: false, events: [], ghost: true , block: '2015/04', weekNumber:  6 },
//   { som: false, eom: true , year: 2015, month: 5, day:  9, week: 6, open: false, close: '定休日'    , holiday: ''          , sow: false, eow: true , events: [], ghost: true , block: '2015/04', weekNumber:  6 },
//   { som: true , eom: false, year: 2015, month: 4, day: 26, week: 0, open: false, close: '定休日'    , holiday: ''          , sow: true , eow: false, events: [], ghost: true , block: '2015/05', weekNumber:  5 },
//   { som: false, eom: false, year: 2015, month: 4, day: 27, week: 1, open: true , close: ''          , holiday: ''          , sow: false, eow: false, events: [], ghost: true , block: '2015/05', weekNumber:  5 },
//   { som: false, eom: false, year: 2015, month: 4, day: 28, week: 2, open: true , close: ''          , holiday: ''          , sow: false, eow: false, events: [], ghost: true , block: '2015/05', weekNumber:  5 },
//   { som: false, eom: false, year: 2015, month: 4, day: 29, week: 3, open: false, close: '昭和の日'  , holiday: '昭和の日'  , sow: false, eow: false, events: [], ghost: true , block: '2015/05', weekNumber:  5 },
//   { som: false, eom: false, year: 2015, month: 4, day: 30, week: 4, open: true , close: ''          , holiday: ''          , sow: false, eow: false, events: [], ghost: true , block: '2015/05', weekNumber:  5 },
//   { som: false, eom: false, year: 2015, month: 5, day:  1, week: 5, open: true , close: ''          , holiday: ''          , sow: false, eow: false, events: [], ghost: false, block: '2015/05', weekNumber:  5 },
//   { som: false, eom: false, year: 2015, month: 5, day:  2, week: 6, open: false, close: '定休日'    , holiday: ''          , sow: false, eow: true , events: [], ghost: false, block: '2015/05', weekNumber:  5 },
//   { som: false, eom: false, year: 2015, month: 5, day:  3, week: 0, open: false, close: '定休日'    , holiday: '憲法記念日', sow: true , eow: false, events: [], ghost: false, block: '2015/05', weekNumber:  6 },
//   { som: false, eom: false, year: 2015, month: 5, day:  4, week: 1, open: false, close: 'みどりの日', holiday: 'みどりの日', sow: false, eow: false, events: [], ghost: false, block: '2015/05', weekNumber:  6 },
//   { som: false, eom: false, year: 2015, month: 5, day:  5, week: 2, open: false, close: 'こどもの日', holiday: 'こどもの日', sow: false, eow: false, events: [], ghost: false, block: '2015/05', weekNumber:  6 },
//   { som: false, eom: false, year: 2015, month: 5, day:  6, week: 3, open: false, close: '振替休日'  , holiday: '振替休日'  , sow: false, eow: false, events: [], ghost: false, block: '2015/05', weekNumber:  6 },
//   { som: false, eom: false, year: 2015, month: 5, day:  7, week: 4, open: true , close: ''          , holiday: ''          , sow: false, eow: false, events: [], ghost: false, block: '2015/05', weekNumber:  6 },
//     // (中略)
//   { som: false, eom: false, year: 2015, month: 7, day:  9, week: 4, open: true , close: ''          , holiday: ''          , sow: false, eow: false, events: [], ghost: true , block: '2015/06', weekNumber: 15 },
//   { som: false, eom: false, year: 2015, month: 7, day: 10, week: 5, open: true , close: ''          , holiday: ''          , sow: false, eow: false, events: [], ghost: true , block: '2015/06', weekNumber: 15 },
//   { som: false, eom: true , year: 2015, month: 7, day: 11, week: 6, open: false, close: '定休日'    , holiday: ''          , sow: false, eow: true , events: [], ghost: true , block: '2015/06', weekNumber: 15 }
// ]
```

最初の行のデータは3/29のもので、最後の行のデータは7/11のものです  
引数で指定した月以外の日データも含まれてますが、これで正常な動作です  
この指定した月以外の日をゴースト日と呼びます  
 (カレンダーでは通常、薄いグレーなど影を薄くするためゴースト日と命名しました。造語です。)  
このデータを利用すると先の1-4は次のように行います  

  1. 最初の要素から表示する。その際、ghost=trueは前月なので目立たないように表示する
  2. sow=trueは週の初めを、eow=trueは週の終わりを示すので、TRタグでくくる
  3. 月末後もそのまま要素を表示する。その際ghost=trueは次月なので目立たないように表示する
  4. 複数月の場合は、som=true・eom=trueがそれぞれ月の初めと最後のデータとして扱う

このように、カレンダーを作成するための情報が揃っています  
Viewコードではデザインだけに集中することができます

具体的なViewコードは、[../example/calendar/calendar1-1.html](../example/calendar/calendar1-1.html)を確認してください  
非常にすっきりとしたViewコードであることが確認できます  
これであれば、もっと複雑な処理（カレンダーを値の入力に使用する・予定を表示させるなど）を追加することが容易になります  


### 引数の説明

  + range
      + 期間を指定します
      + 次の３つの指定の方法があります
          + 年を指定してstartMonthの月から1年分を取得    2015, '2016'など
          + 月を指定 '2015/4', '2015/10'
          + 期間を指定 '2015/4-2016/3'
      + 指定しなかった場合は、本日が含まれる年度の期間になります(プロパティの`startMonth`に依存)

### プロパティの説明

  + block
    + 月ブロックのキー
    + どの月のデータとして取得したかを表します
    + 年月を次のような文字列で示します '2015/01'
  + som  (start of month)
    + 月のはじめ
  + eom  (end of month)
    + 月の終わり
  + sow (start of week)
    + 週のはじめ
  + eow  (end of week)
    + 週の終わり
  + ghost
    + ゴースト日はtrue
  + year
    + 年
    + この年は、取得した月の年を表すのではなく、この日オブジェクト自身の年です
    + どの月のデータとして取得したかは、blockプロパティで判定してください
  + month
    + 月
    + この年は、取得した月を表すのではなく、この日オブジェクト自身の月です
    + どの月のデータとして取得したかは、blockプロパティで判定してください
  + day
    + 日
  + week
    + 曜日 0:日->6:土
  + open
    + 営業日ならtrue
  + close
    + 休業の事由が設定されます
    + 事由に設定される値は`koyomi.closeCause`で確認してください
  + holiday
    + 祝日名、祝日ではない場合はnull
  + weekNumber
    + 週番号
    + メソッド`getCalendarData`で取得されたデータ内だけの週番号です
    + 年度の週番号を得たい場合は、順次処理のなかで別途`getWeekNumber`を使用してください
  + events
    + イベント
    + `koyomi.addEvents`で追加されたイベントです

# イベント

カレンダーにイベントを追加・削除をするためのメソッドが用意されています

## 取得

`{Array} koyomi.getEvents({DATE} date)`  
イベントは文字列の配列です  

## 追加

`{Number} koyomi.addEvent({DATE} date, {String} value)`

戻り値は設定されたイベントが登録されたインデックスです  
指定日にひとつもイベントが登録されていない状態で登録した場合は0が返されます

> `koyomi.close(date)`で休業日に設定している場合は、インデックスが0のイベントが
> 休業理由となり、`koyomi.closeCause(date)`で返されます

## 削除

`{Boolean} koyomi.removeEvent({DATE} date, {Number} index)`

指定したindexのイベントを削除します  
indexを省略した場合は指定日のすべてのイベントが削除されます  
戻り値は削除が成功したかどうかです


# ドキュメント一覧

  + [イントロダクション ../README.md](../README.md)
  + [設定値 ./config.md](./config.md)
  + [フォーマット ./format.md](./format.md)
  + [日時の情報取得・操作 ./calc-date.md](./calc-date.md)
  + [営業日計算 ./calc-biz.md](./calc-biz.md)
  + カレンダー情報 ./calendar.md
  + [祝日 ./holiday.md](./holiday.md)
  + [営業・休業 ./open-close.md](./open-close.md)
  + [補助関数 ./helper.md](./helper.md)
