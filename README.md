# BurpBambdasHero

一個收錄自製 Burp Suite Bambda（Burp Lambda）範例的專案，專為滲透測試與紅隊人員設計，提供更多實用且可客製化的請求過濾邏輯。

## 🧭 專案簡介

Bambda 是 Burp Suite 提供的一種輕量級過濾腳本語言，讓使用者可以撰寫 Java-like 的語法，自由定義顯示哪些 HTTP 請求／回應。它是分析大型測試流量的絕佳利器。

[PortSwigger 官方的 Bambda 專案](https://github.com/PortSwigger/bambdas) 已經提供一些經典的 Bambda filter 範例，但在實際滲透測試或自動化分析中，還有很多進階情境與需求是尚未涵蓋的。

因此，我建立了這個 **BurpBambdasHero** 專案，分享我平時撰寫與使用的 Bambda 腳本，這些腳本可以協助：

- 快速篩選出重要或敏感的 HTTP 請求/回應
- 偵測特定關鍵字、參數、資料格式（如身份證字號、API Key）
- 針對特定測試目標客製化過濾邏輯
