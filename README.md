# BurpBambdasHero

一個收錄自製 Burp Suite Bambda（Burp Lambda）範例的專案，專為滲透測試與紅隊人員設計，提供更多實用且可客製化的請求過濾邏輯。

## 🧭 專案簡介

Bambda 是 Burp Suite 提供的一種輕量級過濾腳本語言，讓使用者可以撰寫 Java-like 的語法，自由定義顯示哪些 HTTP 請求／回應。它是分析大型測試流量的絕佳利器。

[PortSwigger 官方的 Bambda 專案](https://github.com/PortSwigger/bambdas) 已經提供一些經典的 Bambda filter 範例，但在實際滲透測試或自動化分析中，還有很多進階情境與需求是尚未涵蓋的。

因此，我建立了這個 **BurpBambdasHero** 專案，分享我平時撰寫與使用的 Bambda 腳本，這些腳本可以協助：

- 快速篩選出重要或敏感的 HTTP 請求/回應
- 偵測特定關鍵字、參數、資料格式（如身份證字號、API Key）
- 針對特定測試目標客製化過濾邏輯

## 📦 目前收錄的 Bambda 規則

本專案中的每一個 Bambda，皆盡可能同時提供 Target（Site Map） 與 Proxy（HTTP History） 版本。
兩者在語法上略有差異，但偵測邏輯、使用情境與設計概念完全一致，可依實際使用位置選擇對應版本。

#### APIwithParamsJSON200.bambda
篩選出路徑包含 api、請求中帶有參數（GET 或 POST）、回應為 200 OK 且回傳內容為 JSON 格式 的請求，適合用於 API 安全測試、業務邏輯檢測與後續自動化分析。

#### AuthBypassHeaderSmuggling.bambda
發現「非標準 Header 驅動的授權邏輯」，偵測請求中是否包含 X-User、X-Role、X-Auth、X-Forwarded-User 等常見但不標準的授權相關 Header，這類情境在內部 API、微服務或舊系統中特別容易導致 Auth Bypass 或權限錯誤。

#### BusinessLogicPriceTampering.bambda
協助電商、金流與交易邏輯漏洞輔助分析。
當 Request body 中同時出現多個金額或交易相關欄位（如 price、amount、total、discount、quantity），且 Header 中未見簽章、雜湊或 MAC 等保護機制時，標示為可能存在 價格竄改或交易邏輯漏洞 的請求。

#### ParamNameForIDOR.bambda
透過參數名稱方式，快速標示「可能存在 IDOR 的請求」。
根據參數名稱的 heuristic（如 id、uid、user_id、account、order、invoice、profile），搭配參數值型態（單一數字或 UUID），用來找出可能涉及 Insecure Direct Object Reference 的攻擊面。

#### SSRFAttackSurface.bambda
廣義 SSRF 攻擊面探索輔助，透過參數名稱與參數值的方式發現潛在 SSRF 注入點。
不僅限於 http:// 或 https://，透過「參數名稱 + 參數值」的 heuristic，找出可能被用來觸發 Server-Side Request Forgery 的注入點，涵蓋 URL、callback、redirect、webhook 等常見設計模式，並刻意排除 Origin 與 Referer 等高雜訊 Header。
