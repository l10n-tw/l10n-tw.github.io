# 臺灣自由開源 L10N 社群支援站。l10n-tw.github.io

## 建置網站

本網站採用 Jekyll 來產生靜態網頁。您需要安裝[必要軟體](https://jekyllrb.com/docs/installation/)以繼續以下步驟。

### 啟動本機測試伺服器

```shell
bundle exec jekyll serve
```

或

```shell
jekyll serve
```

### 產生部署網站成品

```shell
jekyll build
```

## 變數說明

### 開啟、關閉 AMP 網頁

```
AMP: [true], false 
```

### 警報

_DRAFT: 還沒撰寫完成的訊息,  _PRIVATE: 完全不顯示內文和標題... , 自訂文字

```
INFO: _DRAFT, _PRIVATE, [false], 自訂資訊文字
```
#### 圖標
警報圖標，出自 [Google Material](https://material.io/)。
info (![img](https://fonts.gstatic.com/s/i/materialicons/info/v7/24px.svg)), 
warning (![img](https://fonts.gstatic.com/s/i/materialiconsoutlined/warning/v5/24px.svg))
```
INFO-ICON: [info], warning
```
